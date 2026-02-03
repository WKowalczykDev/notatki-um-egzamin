**Strojenie hiperparametrów** to proces znajdowania optymalnej konfiguracji (learning rate, liczby warstw, dropoutu itp.), która daje najlepsze wyniki na nowych danych. Oto metody i podział danych używany w tym procesie:

---

### **1. Podział danych (fundament strojenia)**

Zanim zaczniesz szukać hiperparametrów, musisz mieć trzy zbiory, nie dwa:

| Zbiór | Po co? | Kiedy używasz? |
|-------|--------|----------------|
| **Treningowy (Train)** | Uczenie wag (backpropagation) | Ciągle, przy każdym eksperymencie |
| **Walidacyjny (Validation)** | Wybór hiperparametrów, early stopping, porównywanie modeli | Po każdej epoce/iteracji tuningowej. Model tego nie widzi podczas uczenia wag. |
| **Testowy (Test)** | Ostateczna, bezstronna ocena gotowego modelu | **Raz**, na samym końcu prac. Jeśli użyjesz go do strojenia, wynik będzie niereprezentatywny (oszustwo/data leakage). |

**Zasada:** Testowy zbiór to „egzamin końcowy” — nie możesz podglądać pytań przed egzaminem. Walidacyjny to „próbne testy”, które pozwalają wybrać strategię nauki.

---

### **2. Metody przeszukiwania przestrzeni hiperparametrów**

#### **A. Grid Search (Przeszukiwanie siatkowe)**
- **Jak działa:** Definiujesz listę wartości dla każdego parametru (np. lr = [0.001, 0.01, 0.1], batch = [16, 32]). Sprawdzasz **wszystkie** kombinacje (kartezjański iloczyn).
- **Wady:** Klątwa wymiarowości. Przy 5 parametrach i 10 wartościach masz $10^5 = 100\,000$ eksperymentów. Kosztowne obliczeniowo.
- **Zalety:** Dokładne (sprawdza wszystko), proste w implementacji.

#### **B. Random Search (Losowe przeszukiwanie)**
- **Jak działa:** Losujesz określoną liczbę kombinacji z przestrzeni parametrów (zamiast wszystkich).
- **Dlaczego często lepszy niż Grid?** Niektóre hiperparametry mają mały wpływ na wynik (np. rodzaj paddingu), a inne ogromny (np. learning rate). Grid traci czas na testowanie 100 wartości bezwartościowego parametru, podczas gdy Random przetestuje 100 różnych wartości kluczowego parametru.
- **Zalety:** Szybszy, często znajduje dobre rozwiązanie przy ułamku kosztu Grid.

#### **C. Hyperband (Algorytm Successive Halving)**
- **Jak działa:** Algorytm „eliminacji”. Zaczynasz od wielu konfiguracji (np. 100), trenujesz je przez **bardzo krótki czas** (np. 1-2 epoki). Zostawiasz tylko najlepsze 50%, trenujesz je dłużej (4 epoki), znowu obcinasz połowę... i tak aż do pełnego treningu finałowych kandydatów.
- **Zalety:** Nie marnuje czasu na oczywiście złe konfiguracje (zbyt duży lr, który od razu eksploduje). Bardzo wydajny przy ograniczonym budżecie obliczeniowym.

#### **D. Bayesian Optimization (Optymalizacja Bayesowska)**
- **Jak działa:** Buduje **model zastępczy** (surrogate model, np. proces Gaussowski), który przewiduje, jaką wydajność da dany zestaw hiperparametrów, bazując na już przetestowanych kombinacjach.
- **Strategia:** Balansuje między **eksploracją** (testowanie nowych, nieznanych regionów) a **eksploatacją** (dokładne przeszukiwanie w okolicach dotychczasowych najlepszych wyników).
- **Zalety:** Najbardziej „inteligentny”. Znajduje optimum przy najmniejszej liczbie prób (najlepszy stosunek jakości do czasu).
- **Wady:** Bardziej złożony obliczeniowo sam proces decyzyjny (ale warte to przy drogich treningach).

---

### **3. Narzędzia (Keras Tuner)**

To biblioteka (API dla TensorFlow/Keras), która implementuje powyższe algorytmy w gotowej formie. Nie musisz ręcznie pisać pętli for do Grid Searcha.

**Co oferuje:**
- `RandomSearch`
- `Hyperband` (zalecany domyślnie — szybki i skuteczny)
- `BayesianOptimization`

Używasz ich, definiując przestrzeń poszukiwań (np. `hp.Int('units', min_value=32, max_value=512, step=32)`), a Tuner sam zarządza procesem, zapisuje wyniki i wybiera najlepszą konfigurację.

---

### **Podsumowanie egzaminacyjne**

| Metoda | Strategia | Główna zaleta | Gdy używać? |
|--------|-----------|---------------|-------------|
| **Grid** | Brute-force (wszystkie kombinacje) | Dokładność | Mała przestrzeń parametrów (<3-4 parametry) |
| **Random** | Losowanie | Efektywność vs Grid | Średnia przestrzeń, gdy niektóre parametry ważniejsze |
| **Hyperband** | Wczesne odcinanie słabych kandydatów | Szybkość, oszczędność zasobów | Duża przestrzeń, ograniczony czas/budżet |
| **Bayesian** | Model probabilistyczny przewidujący wyniki | Najmniej prób potrzebnych do optimum | Bardzo drogie treningi (gdy każda epoka kosztuje) |


#WYKŁAD9 