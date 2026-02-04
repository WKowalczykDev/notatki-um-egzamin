**Uczenie adwersarialne (Adversarial Training)**  
[[Ataki adwersarialne]] | [[FGSM]] | [[Ataki zatruwające]]

### 1. Idea
Najskuteczniejsza obrona przed [[Ataki adwersarialne|atakami adwersarialnymi]] – **samodzielne atakowanie się w trakcie treningu**. Model uczy się na próbkach nieprzyjaznych ($x'$), ale żądamy, by je **poprawnie klasyfikował** (mimo zaburzeń).

**Intuicja:** Jak szczepionka – wstrzykujemy osłabionego wirusa (próbki FGSM), by organizm (model) nauczył się odporności, zanim spotka prawdziwe zagrożenie.

---

### 2. Schemat działania
**Faza treningu:**
1. Dla partii danych $(x, y)$ generujemy odpowiednie $x'$ (np. metodą [[FGSM]]).
2. Łączymy: oryginalne $x$ + zatrute $x'$ w jeden zbiór.
3. Uczymy model minimalizować stratę na **obu typach** danych (celem jest poprawna klasyfikacja $x$ jako $y$ oraz $x'$ jako $y$).

**Kluczowe:** Model widzi zarówno czyste obrazy, jak i ich „atakowane” wersje i musi nauczyć się rozpoznawać obiekt mimo szumu.

---

### 3. Warianty realizacji

| Podejście | Opis | Zalety/Wady |
|-----------|------|-------------|
| **Wstępne generowanie** | Przed treningiem generujemy zbiór próbek adwersarialnych, potem uczymy się na nich jak na zwykłych danych | Prostsze, ale próbki mogą być nieaktualne (model się zmienia) |
| **Dynamiczne (w trakcie)** | W każdej epoce (lub batchu) na bieżąco generujemy nowe $x'$ na aktualnych wagach modelu | Lepsza odporność, ale **znacznie droższe** obliczeniowo |

---

### 4. Ograniczenia

**Koszty obliczeniowe:**  
Jest to forma **brute force** – wymaga wielokrotnego przeliczania gradientów (generowanie $x'$ to dodatkowy forward-backward pass). Trening trwa znacznie dłużej niż standardowy.

**Ryzyko przeuczenia:**  
Model może „nauczyć się na pamięć” konkretnych wzorców szumu użytych w treningu, zamiast generalizować odporność na nowe, niewidziane wcześniej perturbacje. Stąd ważne jest **wielokrotne** generowanie nowych próbek (wariant dynamiczny), a nie użycie jednego, stałego zbioru.

**Niekompletność:**  
Odporność wytrenowana np. na [[FGSM]] nie zawsze chroni przed innymi atakami (PGD, [[ZOO]]) – atakujący może użyć silniejszej metody.

---

### 5. Relacje z innymi strategiami obronnymi
- vs. [[Maskowanie gradientu]]: Tam ukrywamy informacje przed atakującym; tutaj otwarcie uczymy się na próbkach ataku.
- vs. [[Destylacja defensywna]]: Destylacja wygładza przestrzeń decyzyjną poprzez uproszczenie modelu; uczenie adwersarialne „twardo” trenuje na zaburzeniach.
- vs. [[Ataki zatruwające]]: Tam zatrucie ma na celu zepsucie modelu (atak); tutaj zatrucie jest kontrolowane i służy obronie (szczepionka).

**Kluczowe dla egzaminu:**  
Uczenie adwersarialne to najbardziej „naturalna” obrona (data augmentation), ale kosztowna. Nie zapewnia 100% odporności – ataki ewoluują szybciej niż obrony.

#WYKŁAD15 