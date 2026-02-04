**LLM Sampling (Próbkowanie) – Notatka**

---

### **1. Czym jest?**
Mechanizm wyboru **następnego tokenu** na podstawie rozkładu prawdopodobieństwa wygenerowanego przez model. Model produkuje logity, softmax zamienia je na prawdopodobieństwa (suma = 1), a strategia samplingu decyduje, który token faktycznie zostanie wybrany.

---

### **2. Jak działa?**
**Pipeline:** Logity → Softmax → Rozkład prawdopodobieństwa → Strategia wyboru → Token wyjściowy

**Parametr Temperatury (T):** Modyfikuje rozkład przed wyborem:
- **T = 1:** Neutralny (oryginalny rozkład).
- **T < 1:** Wzmacnia różnice (ostrzejszy rozkład, mniej losowości, bezpieczniejsze wybory).
- **T > 1:** Spłaszcza rozkład (więcej losowości, kreatywności, ryzyko błędów).

---

### **3. Metody Samplingu**

| Metoda | Mechanizm | Charakterystyka |
|--------|-----------|-----------------|
| **Greedy (Zachłanna)** | Wybiera token z najwyższym P (zawsze ten sam) | Deterministyczna, bezpieczna, ale powtarzalna (brak kreatywności) |
| **Multinomial** | Losuje zgodnie z rozkładem prawdopodobieństwa | Wprowadza zmienność, tokeny mniej prawdopodobne mają szansę |
| **Top-k** | Ogranicza wybór do k najlepszych tokenów (np. k=5), potem losuje | Balans między jakością a losowością, eliminuje bardzo mało prawdopodobne opcje |
| **Top-p (Nucleus)** | Wybiera najmniejszy zbiór tokenów, których skumulowane P ≥ p (np. 85%) | Dynamiczne, adaptuje się do "pewności" modelu (gdy model jest pewny, bierze mniej opcji) |
| **Beam Search** | Śledzi **b** najlepszych sekwencji (wiązek), wybiera ostatecznie tę o najwyższym skumulowanym P | Optymalizuje całą sekwencję, nie pojedynczy token; lepsza spójność, ale droższe obliczeniowo |
| **Contrastive Search** | Karze za podobieństwo do wcześniejszych tokenów (penalty za powtórzenia) | Zapobiega degeneracji (powtarzaniu się), zachowuje różnorodność i kontekst |

---

### **Podsumowanie**
- **Deterministyczne:** Greedy (przewidywalne).
- **Stochastyczne:** Temperature + Top-k/Top-p (kontrolowana losowość, kreatywność).
- **Sekwencyjne:** Beam Search (optymalizacja długich odpowiedzi).
- **Anty-degeneracyjne:** Contrastive Search (unikanie powtórzeń).

#WYKŁAD11 