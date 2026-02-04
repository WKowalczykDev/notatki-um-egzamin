**Wyjaśnialność modeli ML – od White Box do map istotności**

### 1. White Box vs Black Box
- **White Box (biała skrzynka):** Model „przezroczysty” – widzimy wnętrze (drzewa decyzyjne, regresja). Decyzję możemy prześledzić krok po kroku.
- **Black Box (czarna skrzynka):** Model zamknięty – znamy tylko wejście-wyjście (głębokie sieci). Nie wiemy, co dzieje się w warstwach ukrytych.
- **Cel:** Nawet dla Black Box potrzebujemy **wyjaśnić** (post-hoc), dlaczego model podjął daną decyzję – np. czy rozpoznał kota po uszach, czy po tle zdjęcia.

### 2. Mapy istotności (*Saliency Maps*)
Technika wizualizacji dla obrazów – pokazuje, które piksele były kluczowe dla decyzji modelu.
- **Intuicja:** Liczymy **wrażliwość** – gradient (pochodną) wyjścia względem wejścia. Mówi, jak bardzo zmiana danego piksela zmienia wynik.
- **Wizualizacja:** Nakładamy heatmapę na obraz – czerwone obszary to „to tu patrzył model”.

### 3. Ulepszenia gradientowe
| Metoda | Działanie | Efekt |
|--------|-----------|-------|
| **SmoothGrad** | Dodajemy losowy szum do obrazu, liczymy gradienty dla wielu wersji i uśredniamy | Wygładza mapę, usuwa „szum” – wyraźniejsze główne cechy |
| **Guided Backprop** | Przy propagacji wstecznej **blokujemy ujemne gradienty** (ignorujemy neurony nieaktywowane przez ReLU) | Tłumi nieistotne elementy, zostawia tylko pozytywne wzmocnienia |
![[Pasted image 20260204141831.png]]
### 4. Po co to robić? (Weryfikacja poprawności)
Mapy pozwalają sprawdzić, czy model uczy się **właściwych** wzorców:
- **Poprawnie:** Model patrzy na płuco na zdjęciu RTG.
- **Błąd:** Model patrzy na numer pacjenta w rogu zdjęcia (przeuczenie na artefakty).

---

### Podsumowanie

| Poziom | Co wiemy? | Metoda | Zastosowanie |
|--------|-----------|--------|--------------|
| **White Box** | Struktura + parametry | Analiza reguł | Proste modele (drzewa) |
| **Black Box + Post-hoc** | Tylko decyzja | Mapy istotności | Sieci neuronowe (CNN) |
| **Gradienty** | Wrażliwość na zmianę piksela | Saliency, SmoothGrad, Guided BP | Lokalizacja obiektów w obrazie |

**Kluczowe dla egzaminu:**  
Wrażliwość = gradient. SmoothGrad uśrednia po szumie (wygładza), Guided Backprop odcina ujemne wartości (pokazuje tylko „wspierające” cechy).
#WYKŁAD12 