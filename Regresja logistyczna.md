Regresja liniowa nie bedzie dzialac na wartościach logistycznych - tzn 01 np. detekcja ataków DoS

Model nam może wypluć prawdopodobieństwo i za pomocą regresji logistycznej może nam sklasyfikować do 'tak/ nie'

Najpopularniejsza jest funkcja **sigmoidalna** (g(z) = 1 / (1 + exp(-z)))

W regresji logistycznej gdybyśmy użyli MSE to system utknąłby w lokalnych minimach
- korzystamy z LogLoss (entropia krzyżowa), 
- mierzymy prawdopodobieństwo przewidywania
- a rzeczywistymi etykietami klas

### Funkcja kosztu
Rozwiazaniem dla regresji logistycznej:
chod
**Gdy prawdziwa klasa y=1 :**
- Model mówi hθ​(x)=0.99 (pewny siebie): Koszt=−log(0.99)≈0.01 (mała kara)
- Model mówi hθ​(x)=0.01 (bardzo się myli): Koszt=−log(0.01)≈4.6 (ogromna kara)

**Gdy prawdziwa klasa y=0 :**
- Model mówi hθ​(x)=0.01 (pewny siebie): Koszt=−log(0.99)≈0.01 (mała kara)
- Model mówi hθ​(x)=0.99 (bardzo się myli): Koszt=−log(0.01)≈4.6 (ogromna kara)

#WYKŁAD4
