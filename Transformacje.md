1. nieliniowa
	1. dla naprawy skośności i stabilizacji wariancji
	2. `Jeśli zmienna X ma z targetem Y związek krzywoliniowy (np. wykładniczy lub logarytmiczny), transformacja może go "wyprostować".Przyklad: Wzrost bakterii w czasie jest wykładniczy. Zamiast przewidywać Y od X (co wymaga modelu nieliniowego), transformujesz X logarytmem i nagle prosta regresja liniowa świetnie pasuje.`
2. liniowa
	1. zmieniamy liczby liniowo w przedziale 0,1

### SSN - Samoorganizujące się Sieci Neuronowe
- Opierają się na miarach odległości do wyznaczenia neuronu zwycięscy i aktualizacji wag (dostrajanie)
- Potrzebują znormalizowane dane, dlatego stosujemy 0,1
- W przypadku braku normalizacji dane o wyższej zawartości zdominuja inne dane
## Najczęściej stosowane transformacje
- Z-score (gdy rozkład zbliżony do normalnego)
	- zachowuje informacje o outlierach
	- średnia na poziomie zero
	- odchylenie standardowe 1
	- przedzial [-1;1]
- Unitaryzacja zerowana - normalizacja
	- to samo co z-score tylko 0,1
- normalizacja min-max
	- zła gdy mamy outliery
	- dobra gdy znamy min i max i nie odstaja jakos bardzo

#WYKŁAD2 