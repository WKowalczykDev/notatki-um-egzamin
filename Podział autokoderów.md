Zwykły AE może nauczyć się **kopiowania 1:1** (przeuczenie do funkcji identyczności), omijając kompresję. Poniższe metody **utrudniają** to, wymuszając naukę użytecznych cech.

### 1. Niekompletny (*Undercomplete*)
Tylko architektura – mniej neuronów w warstwie ukrytej niż na wejściu (wąskie gardło).
- **Intuicja:** Dane muszą „przecisnąć się” przez wąskie gardło, więc sieć uczy się kompresji.
- **Ryzyko:** Przy głębokich sieciach nadal może znaleźć „obejście” i skopiować dane bez uczenia się struktury.

### 2. Rzadki (*Sparse*)
Dodajemy **karę za aktywność** neuronów – wymuszamy, by większość była wyłączona (zero).
- **Intuicja:** Sieć może użyć tylko kilku neuronów na raz, więc każdy musi reagować na konkretną, istotną cechę (np. krawędź w obrazie).
- **Efekt:** Wzorzec aktywnych neuronów identyfikuje klaster – przydatne do grupowania danych.

### 3. Odszumiający (*Denoising AE, DAE*)
Na wejście podajemy dane zaszumione, na wyjściu porównujemy z oryginałem.
- **Intuicja:** Skoro na wejściu są śmieci, a chcemy czyste wyjście, sieć **musi** zrozumieć strukturę danych, by „odgadnąć” brakujące informacje.
- **Bonus:** Brakujące wartości traktujemy jak szum – DAE służy do **imputacji danych** (uzupełniania luk).

### 4. Wariacyjny (*Variational AE, VAE*)
Enkoder nie zwraca punktu, lecz **rozkład prawdopodobieństwa** (parametry rozkładu normalnego).
- **Intuicja:** Zamiast sztywnego wektora mamy „chmurę” – losując punkt z tej chmury i dając go dekoderowi, możemy **generować nowe, sensowne dane**.
- **Regularzyacja:** Funkcja straty zawiera dodatkowy czynnik (dywergencja KL), który zmusza rozkłady do grupowania się wokół centrum – dzięki temu przestrzeń ukryta jest ciągła i nadaje się do generowania.

### Tablica porównawcza

| Typ              | Jak utrudniamy kopiowanie?                        | Co sieć uczy się robić?     | Superpower                | Zastosowanie                       |
| ---------------- | ------------------------------------------------- | --------------------------- | ------------------------- | ---------------------------------- |
| **Niekompletny** | Architektura – mało neuronów w środku             | Kompresji stratnej          | Prostota                  | Redukcja wymiarów (non-linear PCA) |
| **Rzadki**       | Kara za aktywność (L1) – większość neuronów = 0   | Reprezentacji rozproszonych | Interpretowalność cech    | Klastrowanie, selekcja cech        |
| **Odszumiający** | Szum na **wejściu** (danych), czyste wyjście      | Odporności na zaburzenia    | Imputacja braków          | Pre-training, oczyszczanie danych  |
| **Wariacyjny**   | Szum w **przestrzeni ukrytej** + rozkład normalny | Modelu prawdopodobnego      | Generowanie nowych próbek | Generative AI, tworzenie obrazów   |

---

**Pułapka na egzaminie:**  
W DAE szum jest na **pixelach/wejściu** (usuwanie szumu z obrazu). W VAE szum jest **wewnętrzny w latent space** (losowanie punktu z rozkładu) – to nie jest czyszczenie danych, tylko mechanizm pozwalający generować.

#WYKŁAD12 