**Uczenie ze wzmocnieniem (RL)**  
*Reinforcement Learning*

### 1. Idea
Agent uczy się przez **własne doświadczenie** w środowisku – wykonuje akcje, dostaje **nagrody** (za dobre ruchy) lub **kary** (za błędy) i maksymalizuje długoterminowy zysk. Nie potrzebuje gotowych etykiet (zbioru uczącego) – **sam generuje dane** poprzez próbę i błąd.

### 2. Problem, który rozwiązuje
- **Brak danych:** Nie wymaga ogromnych zbiorów oznaczonych przez człowieka (jak w klasyfikacji).  
- **Brak wiedzy dziedzinowej:** Nie musimy z góry programować reguł (np. „jak jeździć”). Agent odkrywa optymalną strategię sam.

### 3. Główne zastosowania
| Obszar | Przykład |
|--------|----------|
| **Sterowanie** | Optymalizacja ruchu w sieciach WiFi |
| **Nawigacja** | Autonomiczne samochody, drony |
| **Gry** | AlphaZero (szachy, go) – samodzielna nauka strategii od zera |
| **Finanse** | Automatyczne transakcje giełdowe |

### 4. Charakterystyka procesu
**Douczanie w trakcie użycia (online):** W przeciwieństwie do większości modeli, RL może ciągle adaptować się do zmieniającego się środowiska, ucząc się „na żywo”.
![[Pasted image 20260204161852.png]]

#WYKŁAD14 