**Funkcje kosztu** mierzą, „jak bardzo sieć się myli”. To matematyczna definicja „dobrego” wyniku – algorytm optymalizacji (gradient descent) minimalizuje tę wartość, dostosowując wagi.

---

### **1. Regresja: MSE (Mean Squared Error)**
$$J = \frac{1}{m}\sum(h(x^{(i)}) - y^{(i)})^2$$

**Jak działa:** 
Bierzesz różnicę między predykcją a prawdą, podnosisz do kwadratu i uśredniasz.

**Intuicja:**
- **Kara wykładnicza** – jeśli się pomylisz o 2, koszt to 4; jeśli o 10, koszt to 100. 
- Sieć jest zmuszona unikać **dużych błędów** za wszelką cenę, nawet kosztem drobnych pomyłek w wielu miejscach.

**Kiedy używać:**
- Gdy duże błędy są krytyczne (np. przewidywanie temperatury reaktora jądrowego – błąd o 10 stopni jest znacznie gorszy niż dziesięć błędów o 1 stopień).
- Gdy zakładasz, że błędy mają rozkład normalny (gaussowski).

**Pułapka:** Bardzo wrażliwy na **outliery**. Jedna szalona obserwacja (błąd 100) zdominuje całą funkcję kosztu i „pociągnie” sieć w swoją stronę.

---

### **2. Regresja: MAE (Mean Absolute Error)**
$$J = \frac{1}{m}\sum|h(x^{(i)}) - y^{(i)}|$$

**Jak działa:**
Bierzesz wartość bezwzględną różnicy (moduł) i uśredniasz.

**Intuicja:**
- **Kara liniowa** – błąd o 10 kosztuje dokładnie 10 razy więcej niż błąd o 1.
- Sieć traktuje wszystkie pomyłki „sprawiedliwie” – nie panikuje przy pojedynczych dużych błędach.

**Kiedy używać:**
- Gdy masz **szum** lub outliery w danych (np. błędne pomiary czujników), których nie chcesz „słuchać”.
- Gdy mediana (a nie średnia) jest lepszym estymatorem.

**Różnica vs MSE:** MAE jest bardziej „tolerancyjny” dla ekstremów. Jeśli masz jeden outlier, MSE zmusi sieć, by go dopasować; MAE go zignoruje.

---

### **3. Klasyfikacja binarna: Binary Cross Entropy (Log Loss)**
$$J = -\frac{1}{m}\sum[y^{(i)}\log(h(x^{(i)})) + (1-y^{(i)})\log(1-h(x^{(i)}))]$$

**Jak działa:**
Mierzy „odległość” między rozkładem prawdziwym ($y$ = 0 lub 1) a predykcją sieci ($h(x)$ = prawdopodobieństwo 0-1).

**Intuicja:**
- Gdy $y=1$ (prawda), pierwszy człon aktywny: $-\log(h(x))$. Jeśli sieć mówi „kot z prawdopodobieństwem 0.99”, koszt jest bliski 0. Jeśli mówi „kot z prawdopodobieństwem 0.01” (błąd), koszt eksploduje do $-\log(0.01) \approx 4.6$.
- Gdy $y=0$, działa drugi człon: $-\log(1-h(x))$.

**Dlaczego nie MSE w klasyfikacji?**
MSE dla klasyfikacji (gdzie $y \in \{0,1\}$) daje bardzo małe gradienty, gdy sieć jest pewna siebie (blisko 0 lub 1), nawet jeśli się myli. Cross Entropy daje **silne gradienty** przy błędach – jeśli sieć jest pewna błędnej odpowiedzi (np. mówi 0.99, a powinno być 0), kara jest ogromna i szybko poprawia wagi.

**Kiedy używać:**
- Zawsze przy klasyfikacji binarnej (z sigmoidem na wyjściu).

---

### **4. Klasyfikacja wieloklasowa: Categorical Cross Entropy**
Rozszerzenie na $K$ klas. Zamiast jednego wyjścia (prawdopodobieństwo klasy pozytywnej), masz wektor $K$ prawdopodobieństw (suma = 1, softmax na wyjściu).

$$J = -\frac{1}{m}\sum_{i=1}^{m}\sum_{k=1}^{K}y_k^{(i)}\log(h_k(x^{(i)}))$$

**Intuicja:** Tylko jeden $y_k$ jest równy 1 (prawidłowa klasa), reszta to 0. Więc suma redukuje się do jednego członu: $-\log(\text{prawdopodobieństwo przypisane prawidłowej klasie})$.

**Kara:** Im niższe prawdopodobieństwo przypisane prawidłowej klasie, tym wyższy koszt (logarytm dąży do nieskończoności gdy $p \to 0$).

---

### **Podsumowanie wyboru:**

| Problem | Funkcja | Dlaczego? |
|---------|---------|-----------|
| Regresja (outliery ważne) | **MSE** | Kara za duże błędy jest wysoka |
| Regresja (outliery szkodliwe) | **MAE** | Odporny na wartości odstające |
| Klasyfikacja binarna | **Binary Cross Entropy** | Silne gradienty, dobra probabilistyczna interpretacja |
| Klasyfikacja wieloklasowa | **Categorical Cross Entropy** | Naturalne rozszerzenie na softmax |
#WYKŁAD7 