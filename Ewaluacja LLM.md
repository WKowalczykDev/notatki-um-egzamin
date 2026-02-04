
## **1. Podział metod**

| Typ                        | Opis                                                             | Zastosowanie                       |
| -------------------------- | ---------------------------------------------------------------- | ---------------------------------- |
| **Wewnętrzna (Intrinsic)** | Ocena samego modelu językowego (statystyczna)                    | Szybkie porównanie modeli, tania   |
| **Zewnętrzna (Extrinsic)** | Testowanie w rzeczywistych zadaniach (tłumaczenie, klasyfikacja) | Ostateczna ocena jakości użytkowej |

### **2. Ewaluacja Wewnętrzna – Perplexity (PPL)**
- **Definicja:** Miara „zaskoczenia/zdezorientowania" modelu. PPL = $e^{\text{Cross-Entropy}}$.
- **Interpretacja:** PPL = 100 oznacza, że model przy każdym zgadywaniu następnego słowa jest tak zdezorientowany, jakby wybierał spośród 100 równie prawdopodobnych opcji.
- **Zaleta:** Tania, szybka do obliczenia.
- **Wada:** **Nie koreluje bezpośrednio z trafnością/generowaniem** tekstu (niskie PPL ≠ dobry tekst).
### **3. Ewaluacja Zewnętrzna – Metryki i Metody**

**Automatyczne metryki porównawcze:**
- **BLEU:** Porównuje n-gramy wygenerowanego tekstu z referencją (głównie tłumaczenia).
- **ROUGE:** Recall-oriented (streszczenia) – jak wiele słów ze wzorca zostało odzyskanych.
- **Diversity:** Mierzy różnorodność i unikalność generowanych odpowiedzi (zapobiega powtarzalności).
- **Sentence Embedding:** Porównanie semantyczne wektorów zdań (podobieństwo cosinusowe).

**Oceniający:**
- **Human as a Judge:** Człowiek ocenia jakość (najlepsza jakość, kosztowne, używane przez OpenAI/Google).
- **Model as a Judge:** „Starszy brat" (większy model ocenia mniejszy, np. GPT-4 ocenia inne LLM).

**Benchmarki:**
- **Leaderboards:** Rankingi modeli na zestawach testowych (MMLU, HELM, itp.) sprawdzających konkretne zadania (QA, matematyka, kodowanie).
### **4. Kluczowa różnica**
- **PPL** mierzy, jak dobrze model „przewiduje" dane treningowe (statystyka).
- **Ewaluacja zewnętrzna** sprawdza, czy model **rozwiązuje zadania** poprawnie (użytkowość).


#WYKŁAD11 