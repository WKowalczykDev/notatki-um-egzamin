to technika uczenia nienadzorowanego polegająca na **grupowaniu podobnych obiektów w klastry** bez wcześniejszej znajomości tych grup.

Jak uzyskać dobry wynik
1. Środki klastrów umieszczamy w losowo wybranych k miejscach wśród m punktów
2. Unikamy problemu "pustych punktów"
	1. gdy dany punkt zostanie niepoprawnie losowo przydzielony i nie bedzie w zaden sposob dobrze przydzial danych
	2. losujemy go jeszcze raz
3. Puszczamy algorytm wielokrotnie
	1. przypisujemy na podstawie algorytmu k-means najbardziej podobne punkty
	2. obliczamy końcową funkcję kosztu J

ZALEŻY NAM NA TYM ABY KOŃCOWA KLASTERYZACJA MIAŁA JAK NAJNIŻSZĄ FUNKCJĘ KOSZTU **"J"**
[[Jak wybrać odpowiednią liczbę klastrów]]

`from sklearn.cluster import KMeans`

#WYKŁAD6 