### Epochs, Iterations, Batch Size

**Epoch (epoka):** 
Jedno przejście **wszystkich** przykładów treningowych przez sieć (forward + backprop).

**Batch size (rozmiar paczki):**
Liczba przykładów przetwarzanych **jednocześnie** przed aktualizacją wag. Dlaczego nie pojedynczo? Obliczenia macierzowe na GPU są zoptymalizowane dla batchy – dużo szybsze. Dlaczego nie cały zbiór? Za dużo pamięci i risk utknięcia w minimum lokalnym.

**Iteration (iteracja):**
Jedna aktualizacja wag = jeden batch przetworzony.

**Związek matematyczny:**
$$\text{Iterations} = \frac{\text{Training Set Size}}{\text{Batch Size}}$$

**Przykład:**
- Masz 10 000 zdjęć treningowych
- Batch size = 32
- W 1 epoku wykonasz $10\,000 / 32 \approx 313$ iteracji (aktualizacji wag)

**Batch size – kompromis:**
- **Mały** (np. 16-32): Więcej szumu w gradientach (regularizacja), wolniejsze obliczenia, lepsze generalizowanie
- **Duży** (np. 256-512): Stabilniejsze gradienty, szybsze na GPU, ale ryzyko overfittingu i potrzeba większej pamięci

**Epoki vs zbieżność:**
Nie oznacza to, że więcej = lepiej. Po pewnym czasie sieć zaczyna się „uczyć na pamięć” (overfitting) – stąd early stopping (zatrzymanie gdy wskaźnik na zbiorze walidacyjnym przestaje się poprawiać).

#WYKŁAD7 