**FGSM (Fast Gradient Sign Method)**  
[[Ataki adwersarialne]]

### 1. Idea
Najszybsza metoda białoskrzynkowa – wykorzystuje **gradient funkcji straty względem wejścia** (nie wag!), by znaleźć kierunek najszybszego wzrostu błędu. Modyfikuje obraz o minimalny krok w tym kierunku.

**Analogia:** Jak mapy istotności (CAM), ale zamiast wizualizować, **dodajemy** gradient do obrazu, by zmaksymalizować błąd.

### 2. Mechanizm matematyczny
Dla funkcji straty $J(\theta, x, y)$ liczymy gradient po wejściu $x$:  
$\nabla_x J(\theta, x, y)$ – jak zmiana piksela wpływa na błąd.

**Wzór podstawowy:**  
$x' = x + \epsilon \cdot \text{sign}(\nabla_x J(\theta, x, y))$

$\epsilon$ – współczynnik zaburzenia (kontroluje siłę ataku vs widoczność szumu).

### 3. Warianty

| Wariant | Cel | Wzór | Efekt |
|---------|-----|------|-------|
| **Nieukierunkowany** (*untargeted*) | Odwodzenie od prawdziwej klasy | $x' = x + \epsilon \cdot \text{sign}(\nabla_x J(\theta, x, y_{true}))$ | Model myli się w dowolną stronę |
| **Ukierunkowany** (*targeted*) | Przywodzenie do konkretnej klasy docelowej | $x' = x - \epsilon \cdot \text{sign}(\nabla_x J(\theta, x, y_{target}))$ | Model klasyfikuje jako wybrana klasa (np. pies → samochód) |

**Różnica znaku:**  
$+$ (nieukierunkowany) – wspinamy się po gradiencie straty (maksymalizujemy błąd).  
$-$ (ukierunkowany) – schodzimy po gradiencie straty dla klasy docelowej (minimalizujemy błąd względem $y_{target}$, czyli „wmawiamy” modelowi, że to ta klasa).

---

### 4. Ograniczenia i kontekst
- **Jednokrokowość:** Jeden krok gradientowy – szybki, ale łatwiejszy do obrony niż iteracyjne metody (PGD, BIM).
- **Wrażliwość na $\epsilon$:** Za małe $\epsilon$ – atak nie działa; za duże – szum widoczny dla człowieka.
- **Dane kategoryczne:** Trudniejsze do zastosowania niż na obrazach (piksele ciągłe), bo wymaga modyfikacji wartości rzeczywistych wektora cech.

**Kluczowe dla egzaminu:**  
FGSM to atak **gradientowy po wejściu** (input gradient), nie po wagach. Wykorzystuje **sign** (znak), nie sam gradient – zapewnia równomierny wpływ na wszystkie piksele.

#WYKŁAD15 