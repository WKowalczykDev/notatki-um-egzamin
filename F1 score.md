**F1-score** — metryka **balansu** między Precision a Recall, szczególnie przydatna przy niezbalansowanych klasach. (Ocenia jak dobrze klasyfikator działa)

---

### **Definicja**
Średnia **harmoniczna** Precision i Recall:

$$F_1 = 2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}$$


**Recall** (inaczej: **Czułość**, **Sensitivity**, **True Positive Rate**) — metryka odpowiadająca na pytanie:  
>**„Z wszystkich rzeczywistych pozytywów, ile wykryłem?”**

**Precision** (inaczej: **Dokładność pozytywnych predykcji**) — metryka odpowiadająca na pytanie:  
>**„Z moich pozytywnych predykcji, ile było prawdziwych?”**

- Nie pojawia się nam problem słabszego ogniwa
- W momencie gdy precyzja albo czułość będzie na niezadowalającym poziomie pozwoli nam to zdeklasyfikować cały wynik

---

### **Interpretacja**

| Wartość | Ocena |
|---------|-------|
| 1.0 | Idealny (perfect Precision i Recall) |
| 0.0 | Bezwartościowy (brak TP) |
| 0.5 | Średni (jeden z nich jest słaby lub oba przeciętne) |

---

### **Kiedy używać**
Gdy **oba błędy są ważne** i nie chcesz preferować ani FP, ani FN:
- Detekcja oszustw (fraud) — i przeoczenie (FN), i fałszywy alarm (FP) kosztują
- Systemy rekomendacji — i brak trafnej rekomendacji, i zalewanie śmieciami
- Wyszukiwanie informacji — i brak wyniku, i za dużo nieistotnych wyników

**Nie używaj F1**, gdy priorytetem jest tylko jedno (wtedy optymalizuj samo P lub samo R).
#WYKŁAD7 