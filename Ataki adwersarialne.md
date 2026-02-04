**Ataki adwersarialne (Adversarial Attacks)**  
[[FGSM]] | [[ZOO]] | [[Destylacja modeli]]

### 1. Idea
Sztucznie spreparowane dane wejściowe (**próbki nieprzyjazne**), które wprowadzają model w błąd, pozostając **nieodróżnialne** dla człowieka od oryginałów. Wykorzystują wrażliwość modeli głębokich na precyzyjne zaburzenia wektora wejściowego.

**Wzór ogólny:**  
$x' = x + \delta$  
gdzie $\delta$ – minimalny szum (perturbacja), $| \delta |_\infty < \epsilon$
### 2. Przykłady praktyczne
**Cyfrowe:**  
Mikroskopijny szum na obrazie zmienia klasyfikację „zamek” (prawd. 0,71) → „antena satelitarna” (prawd. 0,99). Dla człowieka obrazy identyczne.

![[Pasted image 20260204185958.png]]
**Fizyczne (real world):**  
Drobne naklejki/graffiti na znakach STOP (niewidoczne zmiany dla oka) powodują błędną klasyfikację w systemach autonomicznych ze skutecznością 66-100%. Atak działa nawet po wydrukowaniu i ponownym sfotografowaniu (transformacje przestrzenne nie niszczą perturbacji).

### 3. Klasyfikacja według dostępu do modelu

| Typ | Dostęp | Metody |
|-----|--------|--------|
| **Biała skrzynka** | Pełna znajomość architektury, wag, gradientów | [[FGSM]], PGD, BIM – ataki gradientowe |
| **Szara skrzynka** | Dostęp do logitów/prawdopodobieństw | [[Destylacja modeli]] (budowa modelu surogatowego) |
| **Czarna skrzynka** | Tylko API (wejście-wyjście) | [[ZOO]], transfer próbek z modelu surogatowego |
### 4. Strategie obronne

| Strategia                     | Mechanizm                                                                               | Ograniczenia                                                                                       |
| ----------------------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| **[[Uczenie adwersarialne]]** | Włączanie próbek nieprzyjaznych do zbioru treningowego (samodzielne atakowanie się)     | Wysokie koszty obliczeniowe (brute force), ryzyko przeuczenia                                      |
| **Maskowanie gradientu**      | Ukrywanie logitów (szum, tylko klasy), użycie modeli nieróżniczkowalnych (drzewa, k-NN) | Nie zawsze możliwe zastąpienie SSN; możliwy **atak transferowy** (próbki działają na różne modele) |
| **[[Destylacja modeli]]**     | Kompresja modelu (uczeń uczy się na logitach nauczyciela) → gładsze gradienty           | Ochrona ograniczona; destylacja może być użyta do ataku (wykradanie wiedzy)                        |

### 5. Ataki czarnoskrzynkowe (gdy brak gradientów)

**Transfer przez model surogatowy:**  
Atakujący odpytuje model (wyrocznię) o logity dla wielu próbek, buduje własny prostszy model (surogat) i na nim generuje ataki. Próbki adwersarialne często **transferują się** między modelami (podobne architektury, np. popularne CNN: ResNet, VGG, MobileNet).

**Właściwość transferu:** Główna groźba – atak wygenerowany na publicznym ResNet często działa na nieznanym modelu producenta (uniwersalność słabości w przestrzeni wysokowymiarowej).

#WYKŁAD15 