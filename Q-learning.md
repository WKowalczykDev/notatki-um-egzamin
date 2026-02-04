**Tablica Q-Learning** - wizualizacja
![[Pasted image 20260204175158.png]]

**Funkcja Q, eksploracja i strategie wyboru akcji**

### 1. Funkcja Q (Action-Value Function)
**Definicja:** $Q^\pi(s,a)$ to oczekiwany zwrot (suma nagród) z wykonania **konkretnej akcji** $a$ w stanie $s$, a następnie postępowania zgodnie z polityką $\pi$.

**Kluczowa różnica od $V(s)$:**  
$V(s)$ mówi „ten stan jest wart 10”. $Q(s,a)$ mówi „jeśli teraz pójdę w lewo, będzie 8, jeśli w prawo – 12”. Pozwala **bezpośrednio porównywać** akcje w tym samym stanie.

**Uczenie:** Aktualizacja metodą różnicy czasowej (TD) na podstawie równania Bellmana – poprawiamy $Q$ na podstawie nagrody $r$ i najlepszego $Q$ ze stanu następnego.

---

### 2. Dylemat eksploracji vs eksploatacji
Agent musi balansować między wykorzystaniem wiedzy a poszukiwaniem nowej.

| Eksploatacja (*exploitation*) | Eksploracja (*exploration*) |
|-------------------------------|----------------------------|
| Wybieram akcję z **najwyższym** obecnym $Q$ (najlepsza znana). | Wybieram **losowo** lub nietypowo, by sprawdzić alternatywy. |
| Bezpiecznie, ale mogę utknąć w **lokalnym optimum** (przegapię lepszą drogę). | Ryzyko kary, ale szansa na odkrycie **globalnego optimum**. |
| *„Jadę sprawdzoną trasą do pracy”* | *„Zjadam w nieznaną uliczkę, może jest szybciej”* |

---

### 3. Strategie wyboru akcji

#### A. Strategia $\epsilon$-zachłanna (*epsilon-greedy*)
**Mechanizm:**  
Z prawdopodobieństwem $1-\epsilon$ wybieram najlepszą akcję (eksploatacja).  
Z prawdopodobieństwem $\epsilon$ wybieram losowo (eksploracja).

**Charakterystyka:**  
- Prostota, najczęściej stosowana.  
- Wada: losowa eksploracja może testować **głupie** akcje (np. skok w przepaść), nie biorąc pod uwagę ich potencjału.

#### B. Próbkowanie Thompsona (*Thompson Sampling*)
**Mechanizm:**  
Traktuję wartość każdej akcji nie jako pojedynczą liczbę, ale jako **rozkład prawdopodobieństwa** (wyrażający niepewność).  
Losuję próbkę z każdego rozkładu i wybieram akcję z najwyższą wylosowaną wartością.

**Charakterystyka:**  
- **Inteligentna eksploracja:** Akcje o wysokiej niepewności (szeroki rozkład) mają większą szansę być wylosowane i przetestowane.  
- Jeśli akcja jest pewna (wąski rozkład) i dobra, będzie często wygrywać. Jeśli jest nieznana, prawdopodobieństwo jej wyboru rośnie dzięki wariancji.

**Podsumowanie:** $\epsilon$-greedy to losowe rzucanie kością, Thompson Sampling to eksploracja tam, gdzie potencjalny zysk jest najbardziej niepewny (a więc najbardziej obiecujący).

#WYKŁAD14 