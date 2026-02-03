## Sieci splotowe CNN - _ang. convolutional neutral networks_
CNN powstała aby naprawić fundamentalne błędy [[MLP]]  (_ang. Multi-Layer Perceptron_) przy przetwarzaniu obrazów

**Rdzeń działania:**  
Zamiast łączyć każdy z każdym, używa **filtrów (jąder)** — małych macierzy (np. 3×3), które przesuwają się po obrazie i wykrywają wzorce (krawędzie, tekstury).

#### Architektura CNN (hierarchia):
1. **Warstwy splotowe (Conv):** Niskie poziomy (krawędzie, kolory) → Średnie (tekstury, wzory) → Wysokie (kształty, części obiektów).
2. **Warstwy pooling (np. MaxPool):** Zmniejszają rozmiar obrazu, zachowując najważniejsze cechy (invariant to small translations).
3. **Warstwy w pełni połączone (FC = MLP):** Na końcu — spłaszczony wektor cech przekazany do zwykłej sieci MLP, która decyduje „kot/pies”.

| Cecha                      | MLP                                       | CNN                                              |
| -------------------------- | ----------------------------------------- | ------------------------------------------------ |
| **Połączenia**             | Każdy z każdym (gęste)                    | Lokalne (3×3, 5×5), współdzielone                |
| **Liczba parametrów**      | Ogromna (zależy od iloczynu wymiarów)     | Mała (zależy od rozmiaru filtra, nie obrazu)     |
| **Struktura przestrzenna** | Tracona (wektor 1D)                       | Zachowana (2D/3D)                                |
| **Uczenie cech**           | Nie ma wbudowanego — musisz podać ręcznie | Hierarchiczne (sam uczy się krawędzi → obiektów) |
| **Typowe zastosowanie**    | Dane tabelaryczne, klasyfikacja końcowa   | Obrazy, wideo, dane przestrzenne                 |

#### Matematyka
Kluczowe która jest jest przekształceniem użycie operacji splotu (_ang. convolution_), do filtrowania danych.
**Cel**: wykrywanie wzorców (im silniejsza odpowiedź filtru tym lepsze dopasowanie fragmentu wejścia do wzorca)

Używamy splotu a nie mnożenie macierzowo-wektorowe
`Conv2D w tensorflow`

### Efekt:
Łatwiejsza implementacja obliczeń - redukcja parametrów sieci dzięki uwspólnieniu (_ang. parameter sharing_)

#### Struktura działania sieci splotowej
![[Pasted image 20260203074431.png]]

**Omówienie architektury działania**

| Etap              | Warstwa               | Co się dzieje?                                                                            | Wymiary (na obrazku)                                                                |
| ----------------- | --------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **Wejście**       | Input                 | Zdjęcie RGB                                                                               | **36×36×3** (wysokość × szerokość × kanały RGB)                                     |
| **Cecha niska**   | Conv2D                | Filtr 11×11 (jak widać na rysunku) przesuwa się po obrazie wykrywając np. krawędzie       | **26×26×9** (9 filtrów/feature map, rozmiar spadł bo filtr nie wychodzi poza obraz) |
| **Redukcja**      | MaxPool2D             | Bierze maksimum z okna 2×2 → zmniejsza wymiar o połowę, zachowuje najsilniejsze aktywacje | **12×12×9**                                                                         |
| **Cecha średnia** | Conv2D                | Drugi splot na mniejszej mapie — wykrywa wzorce złożone z krawędzi (np. tekstury)         | **12×12×9** (lub mniej, zależnie od stride)                                         |
| **Redukcja 2**    | MaxPool2D             | Znowu zmniejszenie                                                                        | **6×6×9** → potem **2×3×?** (na rysunku pokazane jako mały sześcian przed FC)       |
| **Most**          | **Flatten**           | **Spłaszczenie** — 3D sześcian (2×3×głębokość) zamieniany na wektor 1D (np. długości 12)  | Wektor 1D                                                                           |
| **Decyzja**       | Fully Connected (MLP) | Zwykła sieć neuronowa klasyfikuje wektor cech                                             | Najpierw 4 neurony (hidden), potem 2 (output — klasyfikacja binarna)                |
### AveragePooling vs MaxPooling

Na obrazku widzisz **Max Pooling** (pobiera maksymalną wartość z okna — zachowuje najsilniejszy sygnał).

**Average Pooling** to alternatywa:
- Bierze **średnią** zamiast maksimum.
- Działa jak „rozmywanie” (downsampling zachowujący ogólny poziom aktywacji, nie tylko szczyty).

[[Działanie splotu w CNN]]


#WYKŁAD8 