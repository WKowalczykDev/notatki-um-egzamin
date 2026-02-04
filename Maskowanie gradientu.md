**Maskowanie gradientu (Gradient Masking)**  
[[FGSM]] | [[Ataki adwersarialne]] | [[Destylacja modeli]] | [[ZOO]]

### 1. Idea
Skoro [[FGSM]] i ataki białoskrzynkowe wymagają gradientu $\nabla_x J$ do wyliczenia szumu $\delta$, to **ukryjmy lub zniekształćmy** te gradienty. Strategia polega na uniemożliwieniu precyzyjnego wyliczenia kierunku ataku przez zaciemnienie informacji o „nachyleniu” funkcji straty.

---

### 2. Mechanizmy maskowania

| Metoda | Działanie | Efekt dla atakującego |
|--------|-----------|----------------------|
| **Ukrywanie logitów** | Model zwraca tylko **etykietę końcową** (klasa), nie logity ani prawdopodobieństwa; ewentualnie dodaje szum do wyjść | Brak precyzyjnej informacji o „sile” przekonania modelu – trudniej wyliczyć pochodną |
| **Modele nieróżniczkowalne** | Zamiana SSN na drzewa, lasy losowe, k-NN – modele, dla których gradient **nie istnieje** analitycznie | Metody gradientowe (FGSM, PGD) są technicznie niemożliwe do zastosowania bezpośrednio |

---

### 3. Dlaczego to nie jest skuteczna obrona? (Ograniczenia)

**Nie zawsze możliwe:**  
Nie każdy problem da się rozwiązać drzewami (np. klasyfikacja obrazów wymaga CNN). Ukrywanie logitów w SSN ogranicza użyteczność modelu (np. tracimy confidence score).

**Obchody atakującego:**
- **[[Destylacja modeli|Destylacja jako atak]]:** Atakujący odpytuje zaciemniony model wielokrotnie, buduje model surogatowy (który ma gładkie gradienty) i na nim generuje ataki. Próbki często **transferują się** na oryginalny model.
- **[[ZOO]]:** Nawet bez jawnych gradientów, metody optymalizacji zerowego rzędu (aproksymacja gradientu przez szturchanie) potrafią wytworzyć skuteczne perturbacje – wolniej, ale skutecznie.
- **Transferowość:** Próbki wygenerowane na podobnym, publicznym modelu (np. ResNet) często działają na zamaskowanym modelu prywatnym.

---

### 4. Podsumowanie
Maskowanie to **„bezpieczeństwo przez niejawność”** – utrudnia atak białoskrzynkowy, ale nie zatrzymuje determinowanego przeciwnika. Jest tańsze obliczeniowo niż [[Uczenie adwersjalne]], ale mniej niezawodne (łatwiejsze do obejścia). Stosowane jako dodatkowa warstwa ochrony, nie jako główna strategia.

#WYKŁAD15 