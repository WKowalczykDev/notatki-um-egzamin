Uczenie CNN jest oparte na mechanizmie propagacji wstecznej (backprob)

Rozpoznanie obrazów to złożone zagadnienie <=> jest to trudne, kosztowne (pod względem zasobów np. prądu) do wyuczenia

Rozwiązaniem jest **uczenie transferowe**
- często może być ciężko wyuczyć model "od zera", przez ogromną liczbę danych, które byłyby nam potrzebne jako **przykłady uczące**
- nie potrzebujemy od nowa robić detekcji krawędzi, później detekcji kształtów etc.
- używamy wcześniej przygotowanych modeli, douczając na naszym zbiorze danych
	- **Przykład:**
	- jeżeli chcemy zrobić model rozpoznawania kotów
	- bierzemy model do detekcji kształtów zwierząt
	- douczamy go naszymi kotkami

### Kiedy można zmieniać wagi modelu

W modelu robimy podział na:
- warstwy zamrożone _ang. frozen_
	- ustawiamy na warstwy początkowe modelu - detekcji krawędzi kształtów
	- chcemy żeby te własności pozostały niezmienne
	- zapobiegamy wtedy przeuczeniu (detekcja krawędzi powinna zostać taka sama - teoria sie nie zmienia po naszym douczaniu)
- warstwy douczalne _ang. fine tuned_
	- chcemy aby specyficzne własności poprzedniego modelu były przekształcone na takie, których pożądamy
	- **Przykład:**
	- zmieniamy końcowe warstwy modelu rozpoznającego zwierzęta, aby lepiej rozpoznawał kotki
	- zmieniamy wagi modelu, żeby wykrywał cechy bardziej specyficzne dla kotów
	- np. zawsze szpiczaste uszy, a nie jak u kozy


#WYKŁAD8 