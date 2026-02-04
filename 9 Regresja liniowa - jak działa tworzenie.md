Metoda najmniejszych kwadratów:
- znajdujemy najmniejszy kwadrat odległości wszystkich wartosci od linii regresji

Funkcja kosztu dla dwóch parametrów - jak to zrobić
- algorytm gradient descent [[11 Po co gradient w ML|Po co gradient w ML?]]
- przechodzimy iteracyjnie po przestrzeni - w jakim kierunku?
	1. Sprawdza nachylenie terenu pod stopami (gradient)
	2. Robi krok **przeciwnie do największego wzniesienia** (w stronę najszybszego spadku)
	3. Powtarza proces aż do osiągnięcia dna
 - w zależności od szybkości uczenia się, czyli kroków możemy wyskoczyć poza minimum globalne
 - Jeżeli dane są niezeskalowane to gradient descent nie bedzie dzialac tj. na obrazku
 - ![[Pasted image 20260128180550.png]]

#WYKŁAD3
