Jest to algorytm który ma na celu zmniejszyć wagi sieci aby zminimalizować błąd.
Dobry optymalizator to taki który pozwoli nam zejść do minimum globalnego, a nie tylko lokalnego

Działają one na zasadzie Gradient descent [[11 Po co gradient w ML | Po co gradient w ML]]

Wykorzystujemy różnego rodzaju narzędzi do obrabiania gradientów aby wyjść z minimum lokalnego:
- **Vanilla/Stochastic/Mini-batch** = **Ile danych** używamy do obliczenia jednego gradientu (kierunku kroku)
- **Adagrad/Adam/RMSprop** = **Jak wykorzystujemy** ten gradient (czy krok jest stały, czy adaptacyjny)

"jak wykorzystujemy gradient" ma większe znaczenie do zrozumienia różnych technik!!!

## Momentum – „bezwładność” kulki

**Problem:** Czysty gradient descent „tupie w miejscu” w wąskich dolinach – oscyluje między ścianami (zobacz czerwone strzałki na rysunku), bo gradient wskazuje prostopadle na dno, ale kierunek się zmienia.

**Rozwiązanie:** Dodaj **pamięć ruchu** (jak bezwładność w fizyce). Kulka tocząca się w dół doliny nabiera prędkości i „przejeżdża” przez małe wzniesienia (lokalne minima).

**Jak działa:**
- Nie patrzysz tylko na aktualny gradient (czerwona strzałka), ale dodajesz część poprzedniego ruchu (zielona strzałka – momentum).
- Efekt wynikowy (niebieska strzałka) jest wygładzony – przyspiesza wzdłuż długich, spadzistych płaszczyzn i hamuje przy zmianie kierunku.

**Intuicja:** Jak jazda na rowerze z górki – zamiast skręcać ostro co metr (gradient), lecisz z rozpędem i wychodzisz na prostą.

## Stałe momentum nie jest dobrym rozwiązaniem

**Problem:** Globalny learning rate (jedna wartość α dla wszystkich wag) jest niefajny:
- Niektóre wagi (częste cechy) potrzebują małych kroków, inne (rzadkie) – dużych.
- W płaskich obszarach funkcji kosztu chcesz iść szybko (duży krok), w stromych – wolno (mały krok), żeby nie „przeskoczyć” minimum.

**Rozwiązanie:** Każdy parametr (waga) ma **własny**, dynamiczny learning rate, który zmienia się w czasie treningu.

[[Rodzaje algorytmów adaptacyjnych]]


#WYKŁAD7 