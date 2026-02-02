[[K-nn (K nearest neighbours)]]

- odległość euklidesowa
	- ![[Pasted image 20260202183630.png]]
- odległość manhattan
	- ![[Pasted image 20260202183717.png]]
	- jest to dystans mierzony na jakims gridzie
- odległość minkowskiego pozwala nam rozróżnić manhattan albo euklidesa w zależności od hiperparametru - jak p =1 to jest manhattan jak p=2 to euklides
- **Podobieństwo cosinusowe** - mierzymy kąt między dwoma wektorami, ignorując ich długość
	- **1** → wektory wskazują ten sam kierunek (identyczna orientacja)
	- **0** → wektory są ortogonalne (prostopadłe, brak korelacji)
	- **-1** → wektory przeciwnie skierowane
- **Odległość Hamminga** - jest przydzielane dla danych kategorycznych (binarnych)
	- liczymy jak dużo wartości w dwóch rożnych wektorach się ze sobą zgadza
	 - ![[Pasted image 20260202185926.png]]

#WYKŁAD5 