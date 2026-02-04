Trajektoria działania uczenia ze wzmocnieniem
![[Pasted image 20260204171955.png]]

**Schemat działania Uczenia ze Wzmocnieniem (RL)**

### 1. Podstawowe elementy (pętla interakcji)
Agent **nie** uczy się ze zbioru danych, ale przez interakcję ze **środowiskiem** w dyskretnych krokach czasowych $t$:

| Element | Znaczenie |
|---------|-----------|
| **Stan** $s_t$ | Co agent widzi (obserwacja) w chwili $t$ |
| **Akcja** $a_t$ | Ruch/operacja wybrana przez agenta (sterowanie) |
| **Nagroda** $r_t$ | Sygnał zwrotny: $+1$ (dobrze), $0$ (neutralnie), $-1$ (kara) |
| **Polityka** $\pi$ | Strategia agenta – mapa „w danym stanie wybierz tę akcję" |

### 2. Cykl działania (trajektoria)
W każdym kroku $t$:
1. **Obserwuj** stan $s_t$
2. **Wybierz** akcję $a_t$ według polityki $\pi$
3. **Wykonaj** akcję w środowisku
4. **Otrzymaj** nagrodę $r_t$ i przejdź do nowego stanu $s_{t+1}$

Sekwencja $(s_0, a_0, r_0, s_1, a_1, r_1, ...)$ to **trajektoria** (historia epizodu).

### 3. Kluczowe założenia (Proces Markowski MDP)
- **Czas dyskretny** – działamy w krokach $t=0,1,2...$
- **Własność Markowa** – stan $s_{t+1}$ zależy **tylko** od bieżącego stanu $s_t$ i akcji $a_t$ (nie od całej historii). Środowisko jest „bez pamięci" względem przeszłości.
- **Cel** – maksymalizacja **sumy nagród** (nie tylko bieżącej, ale przyszłych, często z dyskontem).

### 4. Wyzwanie vs Zysk
- **Wyzwanie:** Potrzeba **adekwatnego środowiska** (symulatora lub realnego), w którym agent może popełniać błędy i uczyć się na konsekwencjach.
- **Zysk:** Możemy uzyskać rozwiązania dla problemów, dla których **nie istnieją** gotowe zbiory danych (brak etykiet) – agent sam generuje wiedzę przez próbę i błąd.
#WYKŁAD14 