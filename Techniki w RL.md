RL - Reinforcement Learning [[Uczenie ze wzmocnieniem problematyka]] [[Schemat działania uczenia ze wzmocnieniem]]

### 1. Zwrot (*Return*)  
**Definicja:** Suma wszystkich przyszłych nagród, które agent otrzyma od chwili $t$ do końca epizodu (lub w nieskończoności).  

$$G_t = r_t + r_{t+1} + r_{t+2} + ...$$

**Intuicja:** Agent nie optymalizuje „co dostanę teraz”, ale „ile zgarnę w sumie”.  
*Przykład:* W szachach poświęcasz pionka (nagroda -1 teraz), by zbić królową i wygrać (nagroda +100 za 2 ruchy). Zwrot jest duży, więc ruch jest opłacalny.

---

### 2. Współczynnik dyskontowania ($\gamma$, gamma)  
Parametr $0 \leq \gamma \leq 1$ określający, jak bardzo **przyszłe** nagrody są warte mniej niż **bieżące**.

$$G_t = r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + ...$$

| Wartość $\gamma$ | Znaczenie | Zachowanie agenta |
|------------------|-----------|-------------------|
| **$\gamma \approx 1$** (np. 0.99) | Przyszłość jest prawie tak ważna jak teraz | **Długoterminowe** myślenie (inwestycje, strategia) |
| **$\gamma \approx 0$** (np. 0.1) | Tylko teraz się liczy | **Chciwy** (greedy), krótkowzroczny |
| **$\gamma = 0$** | Wyłącznie bieżąca nagroda | Reaguje tylko na natychmiastowy zysk |

**Dlaczego to robimy?**
- **Stabilność:** W epizodach bez końca (nieskończonych) suma nagród mogłaby rosnąć w nieskończoność. Dyskontowanie ją ogranicza.
- **Realizm:** Lepiej dostać 100 zł teraz niż za rok (czas wartość pieniądza/ryzyko).

**Pułapka:** Zbyt niskie $\gamma$ sprawia, że agent nigdy nie nauczy się strategii wymagających cierpliwości (np. unika strat na początku, by wygrać później).

#WYKŁAD14 