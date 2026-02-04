Ze względu na to co optymalizujemy agent moze sie uczyc na różne sposoby
Bezpośrednio powiązane z z [[Q-learning]]
### 1. Value-based (uczenie wartości)
**Idea:** Uczymy się funkcji $Q(s,a)$ lub $V(s)$, a politykę wyciągamy pośrednio (np. zachłannie wybierając najlepsze $Q$).

- **DQN** (*Deep Q-Network*): Aproksymujemy $Q$ głęboką siecią neuronową (SSN). Agent patrzy na stan (np. obraz z gry) i sieć przewiduje wartość każdej możliwej akcji.
- **Warianty:** Double DQN (redukcja przeszacowania), SARSA (on-policy, uczymy się na bieżąco, nie z pamięci).

**Plus:** Stabilne, dobrze zbadane.  
**Minus:** Problemy z dużymi przestrzeniami akcji (trzeba przeliczyć $Q$ dla każdej akcji).

---

### 2. Policy-based (uczenie polityki)
**Idea:** Bezpośrednio parametryzujemy politykę $\pi_\theta(a|s)$ (np. sieć neuronowa zwraca rozkład prawdopodobieństw akcji) i uczymy się gradientowo **maxymalizacji nagród**.

- **REINFORCE:** „Vanilla” gradient polityki – wykonuj epizod, jeśli wysoka nagroda – zwiększ prawdopodobieństwo podjętych akcji.

**Plus:** Naturalne dla ciągłych przestrzeni akcji (robotyka), stochastyczne polityki.  
**Minus:** Wysoka wariancja gradientów (niestabilne), może utknąć w lokalnym optimum.

---

### 3. Model-based (uczenie modelu)
**Idea:** Najpierw budujemy (lub znamy) **model środowiska** (funkcję przejść $s' = f(s,a)$), potem planujemy w nim jak w symulatorze.

- **MCTS** (*Monte Carlo Tree Search*): Symulujemy wiele możliwych przyszłych trajektorii w drzewie decyzyjnym i wybieramy najlepszą ścieżkę (jak w AlphaGo).
- **MPC:** Model Predictive Control – optymalizujemy akcję na horyzoncie kilku kroków do przodu.

**Plus:** Bardzo sample-efficient (nie potrzeba milionów gier w realu).  
**Minus:** Błąd w modelu się kumuluje („reality gap” – model nie oddaje prawdziwego świata).

---

### 4. Actor-Critic (połączenie Value + Policy)
**Idea:** Dwa modele współpracują:
- **Aktor** (policy-based): wybiera akcję (co robić).
- **Krytyk** (value-based): ocenia wybraną akcję (jak dobrze to było).

Krytyk daje „bazę” (advantage), która redukuje wariancję aktora. Uczą się razem.

- **A3C/A2C:** Asynchroniczni aktorzy uczą się równolegle.
- **PPO** (*Proximal Policy Optimization*): Najpopularniejszy obecnie – „bezpieczny” gradient, nie pozwala na zbyt gwałtowne zmiany polityki.
- **SAC** (*Soft Actor-Critic*): Maksymalizuje zarówno nagrodę, jak i entropię (zachęca do eksploracji).

---

### 5. Hybrydy (Model + Value/Policy)
Wykorzystują model do symulacji, ale uczą się też wartości/polityki na podstawie rzeczywistych danych.

- **AlphaZero:** MCTS (model) + sieć polityki/wartości (deep learning) – uczy się sama grając ze sobą.
- **Dyna-Q:** Przeplata prawdziwe kroki w środowisku z wirtualnymi krokami w nauczonym modelu (data augmentation).

---

### Podsumowanie (co egzaminator może zapytać)

| Podejście | Co się uczy? | Kluczowy algorytm | Gdzie się sprawdza? |
|-----------|-------------|-------------------|---------------------|
| **Value-based** | Tablica/funkcja $Q$ | DQN | Gry dyskretne (Atari) |
| **Policy-based** | Bezpośrednio $\pi(a\|s)$ | REINFORCE, PPO | Robotyka (ciągłe akcje) |
| **Model-based** | Dynamika środowiska | MCTS, MPC | Planowanie, szachy, gdy symulator dostępny |
| **Actor-Critic** | $\pi$ + $Q/V$ razem | A3C, PPO, SAC | Najnowocześniejsze zastosowania (general purpose) |

**Kluczowe:** DQN używa SSN do aproksymacji $Q$. REINFORCE to „czyste” gradienty polityki. Actor-Critic łączy oba światy – stąd najlepsze wyniki w praktyce.


#WYKŁAD14 