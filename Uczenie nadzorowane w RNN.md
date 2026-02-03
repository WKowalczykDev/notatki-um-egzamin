Zamysłem działa tak samo, jednak jako, że istnieje tam iteracyjność:
**Kluczowa różna:** Błąd jest **sumą** błędów ze wszystkich kroków czasowych (lub tylko z ostatniego, zależnie od zadania). Sieć musi zminimalizować łączny koszt, więc każdy krok w czasie „ponosi odpowiedzialność” za swój fragment błędu.

**Czy zamysł się różni od zwykłego backprop?**
**Nie – zamysł jest identyczny:** Gradient descent. Chcesz obliczyć, jak zmiana wag wpływa na błąd końcowy, i poprawić wagi.


#WYKŁAD8 