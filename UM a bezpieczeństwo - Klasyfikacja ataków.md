Ataki na modele ML klasyfikujemy według czterech kryteriów (efekt, cel, sposób, wiedza), które opisują **co się psuje**, **po co**, **jak** oraz **z jakim dostępem** do modelu.

### 1. Efekt ataku (co dzieje się z modelem?)
Rodzaj błędu wywołanego przez zaburzenie.

- **Redukcja zaufania** – model traci pewność poprawnej klasyfikacji (spadek confidence), ale jeszcze nie myli się co do klasy.
- **Błędna klasyfikacja** – wymuszenie dowolnej pomyłki (np. pies → kot).
- **Ukierunkowana błędna klasyfikacja** – wymuszenie **konkretnej**, wybranej przez atakującego klasy (np. pies → samochód). Wymaga precyzyjnej kontroli nad gradientem. [[Ataki ukierunkowane]]
- **Błędna klasyfikacja z modyfikacją wejścia/wyjścia** – ataki typu backdoor: specyficzny wzorzec (trigger) w wejściu powoduje predefined output niezależnie od reszty danych.

### 2. Cel (intencja strategiczna)
Ogólny charakter zamierzonego rezultatu.

- **Ataki skierowane** (*targeted*) – precyzyjne oszukanie modelu w konkretny sposób (np. konkretna etykieta wyjściowa).
- **Ataki nie-skierowane** (*untargeted*) – celem jest jakikolwiek błąd modelu; redukcja ogólnej skuteczności bez wskazywania docelowej klasy.

### 3. Sposób ataku (faza i mechanizm)
W jaki sposób atakujący ingeruje w cykl życia modelu.

- **Ataki polegające na unikaniu** (*evasion*) – modyfikacja danych **testowych/użytkowych** w celu oszukania już wytrenowanego modelu. Nie ingerują w trening. Najpopularniejsze w obróbce obrazów ([[Ataki adwersarialne]], [[FGSM]]).
- **Ataki polegające na zatruciu** (*poisoning*) – wstrzyknięcie złośliwych próbek do zbioru **treningowego** (zmiana statystyk danych). Model uczy się na zatrutych danych i działa szkodliwie w ogóle.
- **Ataki polegające na ekstrakcji informacji** (*exploratory*) – odpytywanie modelu (często czarnoskrzynkowo) w celu skradzenia wiedzy o jego działaniu lub odtworzenia architektury (model surogatowy). [[Destylacja modeli]] (jako atak).
- **Ataki polegające na wnioskowaniu** (*inference*) – ataki na **poufność**: odzyskiwanie informacji o danych treningowych (*membership inference*) lub ich właściwościach.

### 4. Dostępność wiedzy (zakres informacji atakującego)
Jak dużo atakujący wie o wewnętrznym działaniu modelu.

- **Biała skrzynka** (*white-box*) – pełna znajomość: architektura, wagi, gradienty, funkcja straty, zbiór treningowy. Ataki gradientowe typu [[FGSM]] działają tutaj najskuteczniej.
- **Szara skrzynka** (*grey-box*) – częściowa wiedza (np. znamy typ modelu CNN/MLP lub mamy dostęp do wartości logitów, ale nie wag). [[Destylacja modeli]] (budowa modelu surogatowego na podstawie odpowiedzi).
- **Czarna skrzynka** (*black-box*) – brak wiedzy o wnętrzu; dostęp tylko przez API (model jako *wyrocznia*). Wymaga metod bezgradientowych typu [[ZOO]] (zeroth-order optimization) lub transferu próbek adwersarialnych z modelu surogatowego.

---

### Kontekst praktyczny (IDS)
W systemach wykrywania włamań (IDS):
- **Evasion** – subtelna modyfikacja nagłówków pakietów sieciowych, by ominąć filtr.
- **Poisoning** – wstrzyknięcie fałszywych logów treningowych sklasyfikowanych jako „normalne”, by model nauczył się ignorować konkretny atak.
- **Efekt** – zazwyczaj ukierunkowana błędna klasyfikacja (atakt ma być uznany za ruch normalny).

---

### Podstawowe strategie obronne
- [[Uczenie adwersarialne]] – trening na próbkach nieprzyjaznych (samodzielne atakowanie się w celu uodpornienia).
- [[Maskowanie gradientu]] – utrudnienie ataków poprzez ukrycie logitów, dodanie szumu lub użycie modeli nieróżniczkowalnych (drzewa, k-NN).
- [[Destylacja modeli]] – uproszczenie modelu (uczeń) w celu wygładzenia gradientów, co utrudnia generowanie perturbacji.


#WYKŁAD15 