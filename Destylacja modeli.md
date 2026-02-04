**Destylacja modeli (Knowledge Distillation)**  
[[Ataki adwersarialne]] | [[Uczenie adwersarialne]] | [[ZOO]] | [[FGSM]]

### 1. Idea
„Kompresja” dużego, złożonego modelu (**nauczyciel**, *teacher*) do mniejszego, prostszego modelu (**uczeń**, *student*), przy jednoczesnym zachowaniu jak największej części wydajności nauczyciela.

**Intuicja:** Zamiast uczyć się od „zerowych” etykiet (hard labels), uczeń naśladuje „rozmytą” wiedzę nauczyciela – rozkład prawdopodobieństw (logity), który zawiera informacje o podobieństwach między klasami (np. pies i wilk są bardziej zbliżone niż pies i samolot).

---

### 2. Mechanizm działania
Uczeń uczy się na podstawie wyjść nauczyciela, nie oryginalnych danych:

**Funkcja straty:**  
Połączenie:
- **Strata destylacyjna** (KL-divergence/Dywerencja Kullbacka-Leiblera): jak bardzo rozkład logitów ucznia odbiega od nauczyciela.
- **Strata klasyczna** (Cross-Entropy): względem prawdziwych etykiet (opcjonalnie, dla utrzymania dokładności).

**Proces:**  
Nauczyciel (wytrenowany, duży) → generuje logity dla danych treningowych → Uczeń (mały) uczy się reprodukować te logity → Wynik: lekki model o zbliżonej skuteczności.

---

### 3. Warianty destylacji

| Typ | Co się przenosi? | Zastosowanie |
|-----|------------------|--------------|
| **Oparta na odpowiedziach** (*response-based*) | Logity / prawdopodobieństwa wyjściowe | Podstawowa kompresja klasyfikatorów |
| **Oparta na cechach** (*feature-based*) | Reprezentacje z warstw ukrytych (embeddings) | Przenoszenie wiedzy o cechach (np. w CNN) |
| **Oparta na relacjach** (*relation-based*) | Podobieństwa między grupami danych (relacje) | Metryki odległości, rankingi |

---

### 4. Podwójne oblicze: obrona vs atak

#### Destylacja defensywna (*defensive distillation*)
**Mechanizm:** Prostsze modele (uczniowie) mają **gładsze gradienty** – ich przestrzeń decyzyjna jest mniej „pikowata”, trudniej znaleźć skuteczne perturbacje dla [[Ataki adwersarialne|ataków adwersarialnych]].

**Efekt:** Utrudnia generowanie próbek [[FGSM]] – gradienty są „rozmyte”, przez co $x'$ wymaga większych zaburzeń, często widocznych dla człowieka.

#### Destylacja jako atak (*model surogatowy*)
**Kontekst:** [[Ataki adwersarialne|Szara skrzynka]] – atakujący nie zna architektury celu, ale może odpytywać go o logity.

**Mechanizm:** Atakujący buduje własny model (uczeń), który destyluje wiedzę z modelu ofiary (nauczyciel). Powstały **model surogatowy** traktuje jak białą skrzynkę – generuje na nim ataki, które często **transferują się** na oryginalny model (podobna architektura wystarcza).

**Ograniczenia:** Kosztowne (wymaga wielu zapytań), podatne na *model mismatch* (niedopasowanie), skuteczność transferu nie jest gwarantowana.

---

### 5. Relacje z innymi konceptami
- vs. [[Uczenie adwersarialne]]: Destylacja wygładza model (zmiana architektury/struktury), uczenie adwersarialne twardo trenuje na szumie (zmiana danych). Można łączyć obie metody.
- vs. [[ZOO]]: ZOO atakuje bez modelu surogatowego; destylacja pozwala go zbudować, by potem użyć szybszych metod gradientowych.

**Kluczowe dla egzaminu:**  
Destylacja to narzędzie obosieczne – służy optymalizacji (mniejsze modele na telefony/IoT) i obronie (gładkie gradienty), ale może być wykorzystana do kradzieży wiedzy (model surogatowy dla ataków).


#WYKŁAD15 