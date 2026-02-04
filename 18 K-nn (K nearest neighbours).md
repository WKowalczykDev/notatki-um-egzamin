Działa na zasadzie przydzielania każdemu "znalezionemu" elementowi jakiejś **k** ilości sąsiadów i w przypadku rodzaju przydzielania przydzielić jakąś klasę na podstawie:
![[Pasted image 20260202183347.png]]
- dla regresji ->averaging (uśrendnianie)
- dla klasyfikacji -> majority voting (te których k jest najwięcej)

W przypdaku niewielkiej ilości knn model jest w prosty sposób niedoucznony, a jak jest zbyt duży to linia jest bardzo niedouczona

**Zazwyczaj stosujemy k o wartościach 3 do 15**
![[Pasted image 20260202190134.png]]

### Do czego jest wykorzystywany
Uzupełnianie wartości nieznanych cech **(imputacja)** - gdy brakuje nam danych w datasecie

Ale też algorytm ważonych knn (uśrednianie pozycji z wagami)
Systemy rekomendacyjne
Predykcja na niewielkich danych medycznych

#WYKŁAD5 