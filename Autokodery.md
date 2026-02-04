### 1. Definicja i architektura
Nienadzorowana sieć neuronowa składająca się z dwóch części:
- **Enkoder:** Kompresuje dane wejściowe do przestrzeni ukrytej (latent space) o **mniejszej liczbie wymiarów** (bottleneck).
- **Dekoder:** Odtwarza (rekonstruuje) dane oryginalne z reprezentacji ukrytej.

Celem jest znalezienie **najmniejszej liczby wymiarów**, w której można zapisać dane tak, by dało się je jeszcze odtworzyć.

---

### 2. Mechanizm uczenia
- **Kryterium:** Minimalizacja **błędu rekonstrukcji** (np. MSE lub Cross-Entropy) – różnica między wejściem a wyjściem dekodera.
- **Charakterystyka:** Autokoder **niedoskonale** przekopiowuje wejście na wyjście (stratna kompresja). Nauczone reprezentacje są generalizacją, a nie kopią.

---

### 3. Porównanie z PCA [[Redukcja wielowymiarowości]]

| Cecha | PCA | Autokoder |
|-------|-----|-----------|
| **Zasada** | Redukcja wymiarowości | Redukcja wymiarowości |
| **Przekształcenie** | **Liniowe** (szuka hiperpłaszczyzn) | **Nieliniowe** (funkcje aktywacji modelują zakrzywione rozmaitości) |
| **Interpretowalność** | Zachowana (osie = kierunki maksymalnej wariancji) | **Utracona** (przestrzeń ukryta to „czarna skrzynka", wymiary nie mają bezpośredniego znaczenia) |
| **Pojemność reprezentacyjna** | Ograniczona (tylko proste zależności) | **Większa** (potrafi uchwycić złożone, wielowarstwowe struktury danych przy tej samej liczbie wymiarów) |

**Podsumowanie:** AE to „PCA na sterydach" – dzięki nieliniowości potrafią znaleźć bardziej efektywne reprezentacje niż liniowe metody, ale kosztem utraty interpretowalności poszczególnych wymiarów.

#WYKŁAD12 