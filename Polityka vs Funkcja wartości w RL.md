### 1. Polityka (*policy*) π
**Definicja:** Strategia agenta – mówi „co robić w danym stanie”.  
- **Deterministyczna:** $\pi(s) = a$ (w stanie $s$ zawsze wybierz akcję $a$)  
- **Stochastyczna:** $\pi(a|s)$ – rozkład prawdopodobieństwa (np. w 80% w prawo, w 20% w lewo). Suma prawdopodobieństw wszystkich akcji w stanie $s$ musi wynosić 1.

**Kluczowe:** Polityka **nie patrzy wstecz** na już otrzymaną nagrodę, tylko **przyszłe** konsekwencje („co najlepsze teraz, by maksymalizować zwrot”).

**Podsumowanie:** Polityka nie uwzględnia nagrody przypisanej w obecnej chwili czasowej (ta już została przyznana), lecz **optymalną akcję** z punktu widzenia stanu obecnego.

### 2. Funkcja wartości $V^\pi(s)$
**Definicja:** Oczekiwana suma przyszłych nagród (zdyskontowana), jaką agent uzyska **będąc w stanie $s$ i postępując zgodnie z politykę $\pi$**.

**Intuicja:** To „prognoza bogactwa” – ile jeszcze zgarnę, jeśli znajduję się tu i będę grał wg strategii $\pi$?  
- Wysoka wartość = obiecująca pozycja (blisko celu/skarbu)  
- Niska wartość = niebezpieczne/puste miejsce  

**Wariant:** Funkcja $Q^\pi(s,a)$ – wartość wykonania akcji $a$ w stanie $s$, a potem postępowania wg $\pi$
### 3. Problem: Co jest pierwsze – polityka czy wartość?
**Dylemat:**  
- By ocenić $V^\pi(s)$, muszę znać politykę $\pi$ (bo od niej zależy, jakie nagrody dostanę w przyszłości).  
- By znaleźć dobrą politykę $\pi$, muszę wiedzieć, które stany są wartościowe (czyli znać $V$).

**Rozwiązanie – iteracyjne podejście:**

| Metoda | Schemat |
|--------|---------|
| **Iteracja polityki** | 1. Zacznij od losowej polityki $\pi$ <br> 2. Oblicz $V^\pi$ dla wszystkich stanów (ewaluacja) <br> 3. Popraw $\pi$: w każdym stanie wybierz akcję prowadzącą do stanu o najwyższej wartości (poprawa) <br> 4. Powtarzaj 2-3 aż do stabilizacji |
| **Iteracja wartości** | 1. Zacznij od losowych wartości $V(s)$ <br> 2. Aktualizuj $V(s)$ używając równania Bellmana (patrzysz, która akcja daje najlepszy $r + \gamma V(s')$) <br> 3. Na końcu wyciągnij politykę: zawsze wybieraj akcję do najlepszego sąsiada |
### 4. Eksploracja vs Eksploatacja (jak żyć na co dzień?)
**Problemem nie jest tylko policzenie wartości, ale ich odkrycie:**  
- **Eksploatacja:** Wybieram to, co wiem, że działa (najwyższe $Q$).  
- **Eksploracja:** Czasem próbuję losowego ruchu, by sprawdzić, czy nie ma czegoś lepszego.

**W praktyce:** Używamy polityki $\epsilon$-greedy – w $(1-\epsilon)$ przypadków wybieramy najlepszą znaną akcję, a w $\epsilon$ losowo, by nie utknąć w suboptymalnym rozwiązaniu.

**Podsumowanie:** Politykę znajdujemy iteracyjnie – najpierw szacujemy wartości przy obecnej strategii, potem poprawiamy strategię wybierając akcje prowadzące do najcenniejszych stanów, aż do osiągnięcia optimum.

![[Pasted image 20260204173047.png]]

#WYKŁAD14 