[[Polityka vs Funkcja wartości w RL]]

**Uczenie funkcji wartości przez Programowanie Dynamiczne (DP)**

### 1. Idea Dynamic Programming (DP) w Reinforcement Learning (RL)
Zamiast błądzić losowo, wykorzystujemy **strukturę problemu**: wartość stanu $V(s)$ zależy od wartości stanów następnych (równanie Bellmana). Rozwiązujemy to iteracyjnie, „wypełniając tabelę” od końca do początku (lub odwrotnie).
### 2. Paralela z Fibonaccim
**Problem:** Oblicz $F(n) = F(n-1) + F(n-2)$.

**Naiwnie:** Rekurencja – liczysz $F(3)$ wielokrotnie dla różnych gałęzi drzewa (nadmiarowość).  
**DP:** Zapamiętujesz (memoizacja) – raz obliczone $F(3)$ wkładasz do tablicy i używasz przy każdym kolejnym zapytaniu.

**W RL:**  
Stany to jak liczby Fibonacciego. Raz obliczone $V(s')$ (wartość stanu „potomka”) służy do aktualizacji wszystkich stanów „rodziców” prowadzących do niego. Nie liczymy od nowa, **budujemy rozwiązanie z podrozwiązań**.

### 3. Paralela z Problemem Plecakowym
**Problem:** Które przedmioty wybrać, by zmaksymalizować wartość bez przekraczania pojemności?

**Właściwość DP:**  
Optymalne rozwiązanie dla plecaka o pojemności $W$ składa się z **optymalnych rozwiązań dla mniejszych pojemności** ($W - w_i$). Nie musisz sprawdzać wszystkich kombinacji – budujesz tabelę od małych plecaków do dużych.

**W RL (iteracja wartości):**  
$V(s) = \max_a [r + \gamma V(s')]$  
To plecak, gdzie „przedmiotem” jest akcja $a$, a „pojemnością” – dyskontowany zwrot z następnego stanu. Szukasz maksimum po wszystkich akcjach, ale korzystasz z już policzonych $V(s')$ (mniejszych „podplecaków”).

### 4. Kluczowe ograniczenie (model vs. model-free)
**DP wymaga modelu:** Musisz znać dynamikę środowiska (prawdopodobieństwa przejść $p(s'|s,a)$), by policzyć wartość.  
**Gdy modelu nie ma:** Używamy Monte Carlo (próbkowanie epizodów) lub TD Learning – to jak szacować Fibonacciego metodą prób i błędów zamiast wzoru.

**Podsumowanie:**  
Uczenie wartości przez DP to technika **dziel i zwyciężaj z memoizacją** – jak w Fibonaccim – stosowana do stochastycznych procesów decyzyjnych. Rozbijamy problem na podproblemy (stany następne), rozwiązujemy je raz i łączymy wyniki by uzyskać optymalną politykę.

#WYKŁAD14 