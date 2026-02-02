### Gdy chcemy zmienić cechy kategoryczne na liczbowe
1. Label Encoding
	1. Przypisujemy każdej unikalnej kategorii liczbe calkowita - ale wprowadza sztuczna hierarchie kolejna liczba odnosi wrazenie wazniejszej
2. Ordinal Encoding
	1. mały =0 średni = 1 duży 2 - dobrze zrobiona hierarchia
3. One hot encoding
	1. tworzymy kolumnu binarne dla kazdej kategorii -> nie ma fałszywej hierarchii
	2. **Wady** klątwa wielowymiarowowści
	3. Jest idelany dla różnych - równowaznych kategorii nominalnych
4. Binary encoding
	1. Kompromis miedzy label a one hot
	2. kodujemy jako liczby binarne i kazdy osobny bit to nowa kolumna - zamiast 8 mamy lg8 =3 cachy - redukujemy wielowymiarowosc
5. Frequency encoding
	1. Zamienia kategorie na liczbe wystapien
	2. Trzeba uzywać jak bezpośrednio liczba wystapien koleryje z czyms innym
6. Target Mean Encoding
	1. Przykład: Jeśli klienci z miasta X mają średnio 85% szansy na zakup, to "X" → 0.85
    2. **Zaleta**: Silna predykcyjność, niski wymiar
    3. **Wada**: Ryzyko przeuczenia (data leakage), wymaga walidacji krzyżowej

### Gdy chcemy zmienić liczbowe na kategoryczne (feature binning)
 Gdy chcemy skategoryzować przedziały -
 1. unsupervised binning
	 1.  zeby wiek nie byl szerokim ale waskim spektrum - nie znamy targetu
		 1. jest wykorzystywane w drzewach decyzyjnych
	 2. dzielimy na rozne rodzaje liczby wystapien
2. supervised binning
	1. entropy baseddzielimy dane tak zeby zmaksymalzowac roznorodnosc klas - zeby jak najwiecej roznych przypadkow bylo zawarte
 #WYKŁAD2 