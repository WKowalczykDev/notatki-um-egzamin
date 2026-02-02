Backprop to mechanizm **rozliczania** – zaczynamy od końcowego błędu i idąc wstecz przez sieć, ustalamy które neurony (i jakie ich połączenia) są odpowiedzialne za pomyłkę, żeby je skorygować. Bez tego sieć nie wie, które wagi poprawić – zgadywałaby w ciemno.

### **Dlaczego to działa efektywnie?**

Bez backpropagation musiałbyś dla każdej wagi osobno liczyć, jak zmiana o ϵ wpływa na końcowy błąd (metoda różnic skończonych) – przy milionach wag byłoby to niemożliwe obliczeniowo.

Backprop wykorzystuje **strukturę grafu** sieci: obliczasz gradient raz dla wyjścia, a potem „rozdrabniasz” go na czynniki pierwsze przechodząc wstecz, wielokrotnie wykorzystując wyniki z poprzednich kroków. Złożoność zmienia się z wykładniczej na liniową względem liczby warstw.

#WYKŁAD7 