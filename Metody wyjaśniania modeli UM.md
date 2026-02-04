**Metody wyjaśnialności modeli ML – Grad-CAM, SHAP, LIME**

---

### 1. Grad-CAM (Gradient-weighted Class Activation Mapping)

**Schemat działania (intuicja):**
1. **Ostatnia warstwa konwolucyjna** zawiera "mapy cech" – każdy filtr wykrywa coś innego (krawędzie, tekstury, części obiektu).
2. **Pytanie:** Które z tych filtrów zareagowały na klasę "kot"?
3. **Mechanizm:** Liczymy gradient (zmianę) predykcji "kot" względem aktywacji każdej mapy. To mówi: "jeśli ten filtr się zmieni, jak bardzo zmieni się pewność, że to kot?".
4. **Ważenie:** Filtry, które mają duży wpływ na klasę, dostają duże wagi. Mnożymy aktywacje map przez te wagi i sumujemy.
5. **Wynik:** Heatmapa nakładana na obraz pokazuje **regiony** (nie pojedyncze piksele), które „przekonały” model do decyzji.

**Kluczowe:** Działa na ostatniej warstwie konwolucyjnej (przed klasyfikatorem), więc pokazuje semantyczne obszary (np. głowa kota), a nie losowe piksele.

---

### 2. SHAP (SHapley Additive exPlanations)

**Intuicja z teorii gier:**
Wyobraź sobie zespół (koalicję) graczy osiągających zysk. Wartość Shapleya mówi: *ile dokładnie ten konkretny gracz dodał do wspólnego sukcesu?*

**W ML:**
- **Gracze** = cechy (np. waga skorupy, wysokość, piksele).
- **Zysk** = różnica między predykcją modelu dla tego przykładu a średnią predykcją dla całego zbioru (baseline).
- **Rozwiązanie:** SHAP sprawdza wszystkie możliwe kombinacje cech (które są, których brak) i liczy średni marginalny wkład każdej cechy.

**Dlaczego to działa/robi ranking?**
Na wykresie (obraz 7) widzisz **wodospad**:
- Startujesz od wartości bazowej (średnia).
- Każda cecha dodaje lub odejmuje swoją "wartość Shapleya".
- **Długość strzałki** = siła wpływu (ranking).
- **Kolor/kierunek** = niebieski (ujemny, pcha w stronę klasy 0) vs czerwony (dodatni, pcha w stronę klasy 1).
- Suma wszystkich wpływów = finalna predykcja modelu.

**Właściwości:**
- **Lokalnie:** Wyjaśnia jedną konkretną predykcję (dlaczego TEN przykład to klasa A?).
- **Globalnie:** Agregując SHAP-y dla wielu przykładów, dostajesz ranking najważniejszych cech w całym modelu.
- **Sprawiedliwość:** Spełnia aksjomaty teorii gier (np. jeśli dwie cechy są identyczne, dostają ten sam wynik).

---

### 3. LIME (Local Interpretable Model-agnostic Explanations)

**Intuicja:**
Zamiast analizować cały skomplikowany model, tworzysz **lokalne przybliżenie** – prostą regresję liniową, która działa podobnie do Twojego modelu **tylko wokół jednego punktu** (lokalnie).

**Schemat działania:**
1. Wybierasz jeden przykład do wyjaśnienia (np. zdjęcie kota).
2. **Generujesz sąsiadów:** Tworzysz warianty przez zaburzanie/maskowanie fragmentów (szum).
3. **Pytasz czarny model:** Jak klasyfikuje te warianty?
4. **Uczysz model surogatowy:** Na podstawie odpowiedzi czarnego modelu, uczysz prostą regresję liniową (ważysz bliskie przykłady mocniej, dalekie słabiej).
5. **Wynik:** Współczynniki prostej regresji mówią, które cechy (fragmenty obrazu) były kluczowe lokalnie.

**Różnica między LIME a SHAP:**

| Cecha                | SHAP                                                  | LIME                                          |
| -------------------- | ----------------------------------------------------- | --------------------------------------------- |
| **Baza teoretyczna** | Teoria gier (sprawiedliwy podział)                    | Przybliżenie lokalne                          |
| **Dokładność**       | Dokładne wartości (suma wpływów = predykcja)          | Przybliżenie (może nie sumować się dokładnie) |
| **Stabilność**       | Stabilny (deterministyczny)                           | Niestabilny (zależy od losowych perturbacji)  |
| **Zakres**           | Lokalny (pojedyncza predykcja) + globalny (agregacja) | Tylko lokalny (lupka na jednym punkcie)       |
| **Szybkość**         | Wolniejszy (obliczeniowo kosztowny)                   | Szybszy                                       |


**Kiedy co użyć?**
- **SHAP** – gdy potrzebujesz pewności matematycznej i globalnego obrazu ważności cech.
- **LIME** – gdy potrzebujesz szybkiego lokalnego wyjaśnienia „dlaczego model się tu pomylił?” lub gdy SHAP jest za wolny.

---

### Podsumowanie

| Metoda | Co pokazuje? | Poziom | Model-agnostic? |
|--------|-------------|--------|-----------------|
| **Grad-CAM** | Regiony obrazu (heatmapa) | Lokalny (jeden obraz) | Nie (tylko CNN) |
| **SHAP** | Wkład każdej cechy w decyzję (z dokładnością matematyczną) | Lokalny + Globalny | Tak |
| **LIME** | Przybliżony lokalny model (które cechy ważne tu i teraz) | Lokalny | Tak |

**Pułapka egzaminacyjna:**  
LIME i SHAP to **model-agnostic** (działają na każdym modelu), ale Grad-CAM wymaga dostępu do warstw wewnętrznych CNN i gradientów – działa tylko na sieciach neuronowych.
#WYKŁAD12 