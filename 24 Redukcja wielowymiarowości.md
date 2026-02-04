Zastosowania:
- redukcja danych (przyspieszenie, obcięcie kosztów ML)
- wizualizacja

Redukcja w praktyce dotyczy ~ 1000D -> 100D


**Algorytm PCA** - _ang. Principal Component Analysis_
Polega na znalezieniu wektorów wzdłuż których te dane są rozpięte z jak najmniejszym błedem.
Na przykład:
![[Pasted image 20260202194302.png]]
Jak działa PCA???
1. Normalizujemy dane
2. Liczymy macierz kowariancji
	1. Zrozumienie jak cechy się współzmieniają
3. Wyznaczamy wektory i wartości własne macierzy
	1. Szukamy kierunków w danych
	2. Takich w których dane się najbardziej rozciągają
4. Redukujemy wymiar danych
	1. **Zasada**: Tworzymy **nowe cechy** jako kombinacje starych, które lepiej reprezentują strukturę danych.
	2. Łączymy oryginalne cechy w nowe "składowe"
	3. Nowe cechy są **matematycznymi konstrukcjami**, nie mają bezpośredniej interpretacji
    4. Zazwyczaj dają lepszą kompresję niż wybór cech

`from sklearn.decomposition import PCA`
#WYKŁAD6 