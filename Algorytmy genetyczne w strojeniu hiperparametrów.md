### **1. Charakterystyka ogólna**
- **Heurystyka:** Podejście ewolucyjne inspirowane biologią, **nie gwarantuje** znalezienia optimum globalnego.
- **Przewaga:** Doskonale nadaje się do **obliczeń równoległych** (można oceniać wiele rozwiązań jednocześnie).

### **2. Mechanizm algorytmu (4 kroki)**

**Krok 1: Inicjalizacja i Selekcja**
- Generujesz losową **populację** rozwiązań (np. zestawy hiperparametrów).
- Trenujesz/weryfikujesz każde rozwiązanie.
- Odrzucasz słabe, zostawiasz najlepsze (**survival of the fittest**).

**Krok 2: Krzyżowanie (Crossover)**
- Łączysz parametry dwóch dobrych rodziców, tworząc potomstwo.
- *Przykład:* Rodzic A ma 3 warstwy i lr=0.01, Rodzic B ma 5 warstw i lr=0.001. Potomek dostaje 3 warstwy i lr=0.001 (wymiana fragmentów „genomu”).

**Krok 3: Mutacja**
- Losowe zmiany w potomstwie (np. zmiana dropout z 0.3 na 0.5), by wprowadzić różnorodność i uniknąć utknięcia w lokalnym minimum.

**Krok 4: Iteracja**
- Nowa populacja staje się rodzicami. Powtarzasz kroki 2-3 aż do wyczerpania budżetu lub osiągnięcia satysfakcjonującego wyniku.

### **3. Zastosowanie: Strojenie hiperparametrów**
Zamiast testować wszystkie kombinacje (Grid Search) lub losowo (Random Search), GA **ewoluuje** coraz lepsze zestawy parametrów:
- „Geny” = konkretne wartości hiperparametrów (liczba warstw, learning rate, dropout).
- „Dostosowanie” (fitness) = wynik walidacyjny modelu (accuracy, F1).

**Różnica vs Hyperband:** GA tworzy **nowe** konfiguracje przez krzyżowanie/mutację. Hyperband tylko odcina słabe i dłużej trenuje dobre, bez tworzenia nowych kombinacji.

### **4. Podsumowanie egzaminacyjne**
GA to **metaheurystyka ewolucyjna:** populacja → selekcja → krzyżowanie → mutacja → powtórzenie. Używana gdy przestrzeń rozwiązań jest ogromna i nie da się przeszukać wszystkiego (np. strojenie NN, problemy kombinatoryczne).

#WYKŁAD9 