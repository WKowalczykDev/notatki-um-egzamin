| Algorytm                              | Mechanizm                                                                             |
| ------------------------------------- | ------------------------------------------------------------------------------------- |
| **Adagrad**                           | Kumuluje kwadraty gradientów – jeśli cecha często się zmieniała, learning rate maleje |
| **RMSprop**                           | Średnia krocząca kwadratów gradientów (zapomina stare, patrzy na nowe)                |
| **Adam** (Adaptive Moment Estimation) | Łączy **Momentum** (pamięć kierunku) + **RMSprop** (adaptacyjny lr per parametr)      |
| **Adamax/Adadelta**                   | Wariacje Adama (inne normy, brak potrzeby ustawiania learning rate)                   |
**Intuicja Adama:** Wyobraź sobie, że każda waga to osobny pies na smyczy:

- **Momentum** – pies pamięta, w którą stronę szedł poprzednio (bezwładność).
- **Adaptacja** – jeśli teren jest nierówny (gradienty skaczą), pies automatycznie zwolni (zmniejszy krok), żeby nie potknąć się o kamienie.


### RMSprop vs Adam różnica

| Cecha             | RMSprop                                                            | Adam                                                                              |
| ----------------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------------- |
| **Momenty**       | Tylko drugi moment (średnia kwadratów gradientów)                  | Pierwszy (gradienty) + Drugi (kwadraty)                                           |
| **Momentum**      | Brak – krok zależy tylko od aktualnego gradientu                   | Jest – krok zależy od średniej kierunków (bezwładność)                            |
| **Korekta biasu** | Zazwyczaj brak                                                     | Obowiązkowa (kluczowa dla pierwszych iteracji)                                    |
| **Zachowanie**    | „Wolniejszy” na płaskich obszarach, może utknąć w lokalnym minimum | „Przebija się” przez płaskie obszary dzięki pierwszemu momentowi, szybciej zbiega |
- **RMSprop** patrzy tylko na to, „jak bardzo skakały gradienty” (czy teren jest stromy/czubaty). Jeśli wchodzisz w dolinę z płaskim dnem, RMSprop bardzo zwolni, bo gradienty są małe i spokojne – możesz utknąć przed optimum.
- **Adam** dodaje **pierwszy moment** – pamięta kierunek z poprzednich kroków. Nawet jeśli aktualny gradient jest mały (płaskie dno), nadal pędzi z rozpędem z górki (jak kulka z bezwładnością), przejeżdżając przez płaskie minimum globalne.

#WYKŁAD7 