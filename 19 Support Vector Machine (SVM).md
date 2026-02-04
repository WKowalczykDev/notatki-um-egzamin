Tworzy optymalną hiperpłaszczyznę klasyfikującą tzn.
1. Poprawnie klasyfikuje wszystkie punkty treningowe
2. Maksymalizuje margines
	1. tylko punkty leżące na skraju marginesu decydują o położeniu hiperpłaszczyzny

SVN można podzielić na 2:
- hard margin
	- maksymalizacja seperacji skrajnych elementów
- soft margin
	- w przypadku danych nie-idealnie seperowalnych
	- wprowadza zmienne relaksacyjne
	- dają one możliwość istnienia danych źle sklasyfikowanych

Jeżeli mamy problem w klasyfikacją danych które są rozdzielne nieliniowo:
- stosujemy sztuczkę jądrową
- pozwala nam na wygenerowanie dodatkowej przestszeni pozwalającej nam wydzielić dane
![[Pasted image 20260202191838.png]]
#WYKŁAD5 