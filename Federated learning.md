### **Główna koncepcja (Flow)**

Zamiast gromadzić dane w jednym miejscu (jak klasyczne ML), **to model podróżuje do danych**. Dane pozostają tam, gdzie powstały (urządzenia, szpitale, banki).

**Krok po kroku (schemat z slajdu):**

1.  **Rozesłanie (1):** Serwer centralny wysyła **globalny model** (architekturę + wagi) do wielu lokalnych węzłów (np. szpitali A, B, C lub smartfonów).
2.  **Lokalny trening (2):** Każdy węzeł trenuje model **na swoich prywatnych danych**, które **nie opuszczają** lokalnego urządzenia. Powstaje lokalny model.
3.  **Przesłanie wag (3):** Węzły wysyłają z powrotem do serwera **tylko aktualizacje modelu** (gradienty lub nowe wagi), nigdy surowe dane.
4.  **Agregacja (4):** Serwer łączy lokalne modele w nowy, ulepszony globalny model (zazwyczaj przez **uśrednianie parametrów** - *FedAvg*).
5.  **Iteracja:** Proces powtarza się do osiągnięcia zadowalającej dokładności.

**Kluczowa zasada:** *„Instead of data moving to a central place, machine learning models move to the data”*.

---

### **Zastosowania sektorowe**

| Sektor | Typ FL | Opis |
|--------|--------|------|
| **IoT** (Cross-Device) | Rozproszone urządzenia | Smartfony uczące wspólnego modelu klawiatury predykcyjnej, smart home analizujące zużycie energii. Każde urządzenie ma mało danych, ale razem tworzą duży zbiór. |
| **Medycyna** (Cross-Silo) | Instytucjonalna współpraca | Szpitale (jak A, B, C na rysunku) współuczą modelu wykrywania raka na podstawie kart pacjentów. Dane medyczne pozostają w szpitalach (RODO/GDPR), ale model uczy się z ogromnej puli przypadków. |
| **Bankowość** (Cross-Silo) | Konkurencyjna kolaboracja | Banki współpracują przy wykrywaniu fraudów czy ocenie ryzyka kredytowego. Uczą się na lokalnych historiach transakcji, nie ujawniając danych klientów konkurentom. |

---

### **Plusy i ograniczenia**

**Na plus:**
- **Prywatność i ochrona danych:** Dane nigdy nie opuszczają źródła (eliminacja ryzyka wycieku przy centralizacji).
- **Skalowalność:** Wykorzystanie rozproszonych zasobów obliczeniowych (telefony, lokalne serwery).

**Ograniczenia:**
- **Spójność danych (Non-IID):** Dane w różnych szpitalach/bankach mogą być bardzo różne (inna populacja, inne standardy), co utrudnia zbieżność modelu globalnego.
- **Heterogeniczność urządzeń:** Różne moce obliczeniowe (szybki serwer vs. słaby telefon), różne czasy odpowiedzi.
- **Koszty komunikacji:** Przesyłanie wag wielokrotnie generuje duży ruch sieciowy (przepustowość, opóźnienia).

---

### **Narzędzia (Frameworki)**
- **TensorFlow Federated (TFF)** – Google
- **PySyft** – Biblioteka Python z szyfrowaniem homomorficznym (dodatkowa warstwa bezpieczeństwa)
- **Flower** – Uniwersalny framework (współpraca z PyTorch, TF, scikit-learn)
- **NVIDIA FLARE** – Rozwiązanie dla sektora medycznego/enterprise

**Podsumowanie:** FL pozwala uczyć się na „nieuczonych” danych – model podróżuje między silosami (instytucjami) lub urządzeniami IoT, zachowując prywatność użytkowników i zgodność z regulacjami.

#WYKŁAD9 