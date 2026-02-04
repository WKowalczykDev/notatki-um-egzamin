**ZOO (Zeroth Order Optimization)**  
[[Ataki adwersarialne]] | [[FGSM]] | [[Destylacja modeli]] | [[Czarna skrzynka]]

### 1. Idea
Metoda ataku **czarnoskrzynkowego** (brak dostępu do wnętrza modelu), która nie wymaga ani znajomości architektury, ani budowania [[Destylacja modeli|modelu surogatowego]]. Wykorzystuje **optymalizację zerowego rzędu** – działa wyłącznie na podstawie wartości funkcji celu (prawdopodobieństwa klas), bez jawnych gradientów.

**Intuicja:** Jak badanie terenu na oślep – nie widać mapy (gradientów), ale można „szturchać” model małymi zmianami wejścia i obserwować, czy wyjście rośnie czy maleje.

---

### 2. Mechanizm – aproksymacja gradientu
Skoro nie mamy gradientu $\nabla_x J(x)$, przybliżamy go ilorazem różnicowym (symetrycznym), zmieniając **jedną cechę/piksel na raz**:

$$\nabla_{x^{(i)}} J(x) \approx \frac{J(x + \Delta \cdot e_i) - J(x - \Delta \cdot e_i)}{2\Delta}$$

Gdzie:
- $e_i$ – wektor bazowy (1 na pozycji $i$, 0 reszta), czyli sztucznie zmieniamy tylko $i$-ty piksel/cechę.
- $\Delta$ – mała stała (krok różniczkowania).
- $J$ – funkcja straty (błąd klasyfikacji dla wybranej klasy).

**Proces:** Dla każdego piksela w obrazie (lub cechy w wektorze) wykonujemy **dwa zapytania** do modelu (plus i minus $\Delta$), by oszacować, w którą stronę zmienić wartość, by zwiększyć błąd.

---

### 3. Kontekst i ograniczenia

**Zalety:**
- **Prawdziwy black-box:** Działa na dowolnym API, które zwraca prawdopodobieństwa (lub nawet tylko klasy).
- **Bez transferu:** Nie zakłada podobieństwa do publicznych modeli (w przeciwieństwie do ataków transferowych).

**Wady (krytyczne):**
- **Koszt obliczeniowy:** Dla obrazu 1000 pikseli potrzeba ~2000 zapytań na jedną iterację aktualizacji. Atak na jeden przykład może wymagać tysięcy zapytań – **niepraktyczny przy ograniczonym API** (koszty, rate-limits).
- **Wysoka wymiarowość:** W przestrzeniach wysokowymiarowych (obrazy) metoda jest bardzo wolna zbieżna w porównaniu do gradientowych metod typu [[FGSM]].

---

### 4. Porównanie podejść black-box

| Metoda | Wiedza | Mechanizm | Koszt zapytań |
|--------|--------|-----------|---------------|
| **[[Destylacja modeli]]** | Szara (logity) | Budowa surogatu, potem atak gradientowy | Wysoki (tysiące na trening surogatu) + niski na atak |
| **ZOO** | Czarna (tylko I/O) | Bezpośrednia aproksymacja gradientu | Bardzo wysoki (tysiące na jedną próbkę) |
| **Transfer próbek** | Czarna + publiczne dane | Atak na podobny model, przeniesienie na cel | Niski (jednorazowy atak na surogat) |

---

### Kluczowe dla egzaminu
ZOO to „brute force gradientowy” – zamiast liczyć pochodne analitycznie (jak w [[FGSM]]), szacujemy je eksperymentalnie, płacąc ogromną ceną w liczbie zapytań. Stosowany, gdy nie da się zbudować [[Destylacja modeli|modelu surogatowego]] (np. model celu jest zbyt unikalny, a API zwraca tylko klasy bez logitów).

#WYKŁAD15 