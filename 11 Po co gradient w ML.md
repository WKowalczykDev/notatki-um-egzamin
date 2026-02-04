### Po co w ogóle gradient w ML? (Głębsza odpowiedź)

Zadaj sobie pytanie: _Dlaczego w ogóle istnieje "uczenie" się? Czemu nie po prostu "obliczamy" odpowiedź?_

**Odpowiedź:** Bo w 99% problemów ML (szczególnie gdy przechodzisz od regresji do sieci neuronowych) **nie ma arkusza kalkulacyjnego, który podałby rozwiązanie**.

Gradient to uniwersalna metoda **"uczenia się przez próbowanie"** zamiast "obliczania przez wzór":
1. **Zamiast rozwiązywać równanie** (co w logistycznej jest niemożliwe), **"czujesz"** kierunek poprawy (gradient).
2. **Robisz mały krok** w tym kierunku.
3. **Sprawdzasz** czy był dobry (funkcja kosztu spadła).
4. **Powtarzasz** aż będzie dobrze.

To różnica między:

- **Inżynierem**, który projektuje most obliczając wszystko z równań (tylko w prostych problemach to działa)
- **Rzemieślnikiem**, który szlifuje rzeźbę, patrzy co wyszło, poprawia trochę, patrzy znowu — aż będzie idealnie (to jest gradient descent)

#WYKŁAD4 #WYKŁAD3 