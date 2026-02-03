
**Generacja danych (Data Augmentation)** — syntetyczne powiększanie zbioru treningowego przez **transformację istniejących próbek** (nie tworzenie od zera).

---

### **1. Mechanizm**
Zamiast zbierać nowe dane (kosztowne/czasochłonne), stosujesz **deterministyczne lub losowe przekształcenia**, które zmieniają „formę” danych, ale **nie zmieniają etykiety (label)**.

| Typ danych | Przekształcenia (przykłady) | Co się nie zmienia? |
|------------|----------------------------|---------------------|
| **Obrazy** | Rotacje, odbicia lustrzane, zmiana jasności/kontrastu, przycięcia (crop), szum | Klasa obiektu (kot to nadal kot, tylko obrócony) |
| **Audio** | Zmiana tonu (pitch shift), zmiana tempa (time stretch), dodanie szumu tła, inwersja fazy | Wypowiadane słowo/dźwięk |
| **Tekst** | Zamiana słów na synonimy, losowe usunięcie/wstawienie słów, back-translation (przetłumacz i wróć) | Sentyment/klasa (pozytywny tekst pozostaje pozytywny) |

**Efekt:** Sieć widzi „nowe” przykłady, ale uczy się **inwariantności** (np. kot to kot niezależnie od kąta czy oświetlenia), co zapobiega przeuczeniu (overfitting) na sztywne, oryginalne pozycje pikseli.

---

### **2. Kluczowa pułapka: Niezbalansowane klasy**
Zwróć uwagę na uwagę ze slajdu: *„to niekoniecznie pomaga w przypadku niezrównoważonego zbioru danych”*.

**Dlaczego?**
Standardowa augmentacja stosowana globalnie **zachowuje proporcje klas**.
- Masz 1000 zdjęć kotów i 10 psów.
- Augmentujesz 10x obie klasy → masz 10 000 kotów i 100 psów.
- Stosunek nadal 100:1. Model nadal dominuje koty.

**Rozwiązanie:** Augmentacja musi być **selektywna** (oversampling + augmentacja tylko klasy rzadkiej) lub używasz metod typu **SMOTE** (generowanie syntetycznych próbek w przestrzeni cech, nie tylko transformacja obrazu).

---

### 3. Podsumowanie
- **Cel:** Regularizacja (zapobieganie overfittingowi) przy małym/mało różnorodnym zbiorze.
- **Metoda:** Transformacje zachowujące semantykę (label).
- **Limitacja:** Nie naprawia sama w sobie **nierównowagi klas** — musisz celowo generować więcej danych dla klasy mniejszościowej.


#WYKŁAD8 