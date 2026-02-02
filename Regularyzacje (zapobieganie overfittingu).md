![[Pasted image 20260203003233.png]]
### **1. Regularizacja L2 (Ridge)**
**Jak działa:** Dodaje do funkcji kosztu „karę” proporcjonalną do **kwadratu** wag: $\lambda \sum w_j^2$.

**Mechanizm:** Sieć jest zmuszona do minimalizowania nie tylko błędu predykcji, ale też wielkości wag. Duże wagi są „drogie” – koszt rośnie z ich kwadratem. Optymalizator więc preferuje **małe, rozproszone wartości** wielu wag zamiast kilku ogromnych.

**Intuicja:** Duże wagi oznaczają, że sieć „przekształca” pojedyncze cechy drastycznie (przeuczenie na szczegół). L2 wymusza „łagodniejsze” podejście – każdy neuron bierze lekki udział w decyzji, nikt nie dominuje.

**Efekt:** Wagom nie pozwala się „rozrosnąć”. Sieć uczy się gładkich, ogólnych funkcji.

---

### **2. Regularizacja L1 (Lasso)**
**Jak działa:** Dodaje karę proporcjonalną do **modułu** wag: $\lambda \sum |w_j|$.

**Mechanizm różniący się od L2:** Moduł (a nie kwadrat) sprawia, że kara liniowo rośnie z wagą. To sprawia, że optymalizator **preferuje zerowanie wag** (całkowite usunięcie połączenia) nad ich zmniejszanie.

**Intuicja:** L2 rozsmarowuje wagę na wszystkie cechy (wszystkie są małe). L1 **selekcjonuje** cechy – wybiera kilka istotnych i eliminuje resztę (wagi stają się dokładnie zerami).

**Efekt:** Sieć staje się „rzadka” (sparse) – niektóre neurony faktycznie odpadają. To automatyczna selekcja cech.

---

### **3. Dropout**
**Jak działa:** W każdej iteracji (batch-u) losowo **wyłączamy** (zerujemy) zadaną część neuronów (np. 20-50%) wraz z ich połączeniami. Sieć uczy się na „okaleczonej” wersji siebie.

**Dlaczego to działa:**
- **Wymuszona redundancja:** Nie możesz polegać na jednym „genialnym” neuronie, bo może zostać wyłączony w następnej iteracji. Każdy neuron musi nauczyć się czegoś użytecznego, ale nie może być „niezastąpiony”.
- **Ensembling:** Efektywnie trenujesz jednocześnie wiele różnych, mniejszych sieci (każda to inna kombinacja aktywnych neuronów). Końcowa sieć to średnia tysięcy pod-sieci.

**Intuicja:** Jak szkolenie zespołu sportowego, gdzie w każdym treningu losowo brakuje jednego zawodnika. Reszta musi nauczyć się grać bez niego – zespół staje się bardziej elastyczny i mniej uzależniony od indywidualnych gwiazd.

**Uwaga:** Dropout działa tylko podczas treningu. W czasie predykcji (testu) wszystkie neurony są aktywne (ale często skalowane, by zachować średnią siłę sygnału).

---

### **4. Early Stopping**
**Jak działa:** Monitorujesz błąd na zbiorze **walidacyjnym** (nie treningowym!). Gdy ten błąd przestaje spadać i zaczyna rosnąć – zatrzymujesz trening.

**Mechanizm:** Overfitting zaczyna się, gdy sieć „ma już czas” na zapamiętanie szczegółów treningowych. Early stopping przerywa uczenie w **punkcie optymalnym** – tuż przed momentem, gdy sieć zaczyna się przeuczać.

**Intuicja:** Jak gotowanie makaronu. Trening to czas gotowania. Zdejmujesz makaron z ognia (zatrzymujesz uczenie) w momencie, gdy jest al dente (najlepsza generalizacja), a nie wtedy, gdy zaczyna się rozgotowywać (overfitting).

**Implementacja:** W Keras (i innych frameworkach) to callback, który zapisuje najlepsze wagi (checkpoint) i przywraca je, gdy przez X epok nie ma poprawy na validacji.

---

### **Podsumowanie porównawcze**

| Metoda | Co „karze”? | Efekt na sieci | Gdzie działa? |
|--------|-------------|----------------|---------------|
| **L2** | Duże wagi | Małe, równe wagi dla wszystkich cech | Funkcja kosztu |
| **L1** | Istnienie wag | Rzadka sieć (niektóre wagi = 0) | Funkcja kosztu |
| **Dropout** | Zależność od pojedynczych neuronów | Redundancja, ensembling | Architektura (przełączanie neuronów) |
| **Early Stop** | Zbyt długie uczenie | Zatrzymanie przed zapamiętaniem | Proces treningu (czas) |

**W praktyce:** Używa się ich razem – np. L2 + Dropout + Early Stopping to standardowa trójka zapobiegająca przeuczeniu.

L1 jest raczej żadko używane, ale przydaje się w wyborze cech w danych wysokowymiarowych, przez co jesteśmy w stanie określić co tak naprawdę wpływa
Przydaje się również przy ograniczonym sprzęcie

#WYKŁAD7 