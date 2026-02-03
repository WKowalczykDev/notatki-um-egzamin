![[Pasted image 20260203011856.png]]**Notatka: Postępowanie przy niezbalansowanych klasach (imbalanced data)**

---

### **1. Najpierw: wybierz właściwą metrykę (zależy od kosztu błędu)**

| Scenariusz | Priorytet | Metryka | Przykład |
|------------|-----------|---------|----------|
| **FP kosztowne** (fałszywy alarm) | Wysokie Precision | Precision, FPR (False Positive Rate) | Spam filter (nie chcesz ukryć ważnego maila), niepotrzebna biopsja u zdrowego |
| **FN kosztowne** (przeoczenie) | Wysokie Recall | Recall, TPR (True Positive Rate), F1 | Wykrywanie raka (nie możesz przeoczyć chorego), atak hakerski, defekt fabryczny |
| **Oba kosztowne** | Balans | **F1-score**, AUC-ROC, AUC-PR | Detekcji oszustw finansowych (i przeoczenie, i fałszywy alarm kosztują) |

---

### **2. Techniczne rozwiązania (Keras/PyTorch)**

#### **A. Wagi klas (najprostsze)**
Kara za błąd na rzadkiej klasie większa:
```python
# Keras: klasa 1 (rzadka) ma wagę 99x większą niż 0
model.fit(X, y, class_weight={0: 1, 1: 99})
```
**Efekt:** Sieć boi się FN (przeoczenia rzadkiej klasy), bo błąd kosztuje 99x więcej.

#### **B. Przesunięcie progu (Threshold tuning)**
Nie używaj domyślnego 0.5:
- **Chcesz wysoki Recall (unikać FN):** Próg niższy, np. 0.2 (łatwiej zaklasyfikować jako pozytyw)
- **Chcesz wysokie Precision (unikać FP):** Próg wyższy, np. 0.8 (trudniej zaklasyfikować jako pozytyw)

#### **C. Resampling danych**
| Metoda | Kiedy? | Ryzyko |
|--------|--------|--------|
| **Oversampling** (powielanie/SMOTE rzadkiej klasy) | Mało danych ogółem | Overfitting na powielonych przykładach |
| **Undersampling** (usuwanie dominującej klasy) | Dużo danych | Utrata informacji (wyrzucasz poprawne dane) |
| **Hybrid** (np. SMOTEENN) | Standard | Najbezpieczniejszy kompromis |

#### **D. Inna funkcja kosztu**
Zamiast `binary_crossentropy` — **Focal Loss** (karze łatwe przykłady dominującej klasy, skupia się na trudnych, rzadkich).

---

### **3. Scenariusze egzaminacyjne**

**Scenariusz: Rak (1% chorych)**
- **Cel:** Maksymalny Recall (nie przeoczyć chorego)
- **Akceptowalne:** Niskie Precision (zdrowy dostaje fałszywy alarm i robi badania kontrolne)
- **Rozwiązanie:** Wysoka waga klasy 1, próg 0.3, optymalizacja F1

**Scenariusz: Spam (90% spamu)**
- **Cel:** Wysokie Precision (nie wyrzucić ważnego maila do spamu)
- **Akceptowalne:** Niski Recall (przeoczenie kilku spamów)
- **Rozwiązanie:** Wysoka waga klasy 0 (ważne maile), próg 0.9

**Scenariusz: Fraud transakcyjny (0.1%)**
- **Cel:** Balans (oba błędy kosztują pieniądze)
- **Rozwiązanie:** SMOTE + F1-score + AUC-PR ( Precision-Recall curve lepsza niż ROC przy imbalance)

---

### **4. Czego NIE robić**
- **Nie optymalizuj Accuracy** — przy 99:1 zawsze będzie 99% przez głupie przypisanie wszystkich do dominującej klasy.
- **Nie ignoruj problemu** — „dummy classifier” (zawsze mów „zdrowy”) ma świetną accuracy i bezwartościową użyteczność.

#WYKŁAD7 