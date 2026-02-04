### **1. Inicjalizacja parametrów: dlaczego losowe, a nie zera?**

**Problem symetrii:**
Jeśli zainicjalizujesz wszystkie wagi na **zero** (lub tę samą stałą), każdy neuron w danej warstwie otrzymuje identyczne gradienty podczas backpropagation i uczy się **identycznych** cech. W efekcie cała warstwa zachowuje się jak pojedynczy neuron – tracisz głębokość sieci (brak różnorodności reprezentacji).

**Rozwiązanie:** Losowe wartości początkowe (z rozkładu np. normalnego lub jednostajnego) łamią symetrię – każdy neuron startuje z innej „perspektywy” i uczy się innych wzorców.

### **2. Wariancja inicjalizacji – złoty środek**

**Za mała wariancja (bliskie zeru):**
- Sygnały przepływające przez sieć stają się coraz słabsze
- Gradienty zanikają (vanishing gradient)
- Uczenie zwalnia lub zatrzymuje się (szczególnie w głębokich warstwach)

**Za duża wariancja (duże losowe wartości):**
- Sygnały eksplodują (rosną wykładniczo przez warstwy)
- Gradienty stają się ogromne (exploding gradient)
- Sieć „wariuje” – wagi skaczą chaotycznie, brak zbieżności

**Optymalna wariancja (Glorot/Xavier):**
Inicjalizacja szkaluje wariancję względem liczby neuronów wejściowych i wyjściowych:
$$Var(W) = \frac{2}{n_{in} + n_{out}}$$

**Intuicja:** Jeśli do neuronu wchodzi 100 połączeń, każde powinno mieć małą wagę (~0.1), żeby suma ważona nie „wybuchła”. Jeśli wchodzi 10 połączeń – mogą być większe (~0.3).

**Keras:** `GlorotUniform` (Xavier) domyślnie ustala zakres $[-\sqrt{\frac{6}{n_{in}+n_{out}}}, \sqrt{\frac{6}{n_{in}+n_{out}}}]$.

### **3. Normalizacja danych wejściowych (feature scaling)**

**Dlaczego krytyczne:**
Sieć używa tych samych wag dla wszystkich cech. Jeśli cecha A ma zakres 0-1, a cecha B 0-10000, gradienty będą dominowane przez cechę B. Optymalizator będzie „tańczył” wzdłuż wąskich dolin funkcji kosztu (wolna zbieżność).

**Rozwiązanie:**
- **StandardScaler** (zero mean, unit variance): $\frac{x - \mu}{\sigma}$
- Lub **MinMaxScaler** (0-1): $\frac{x - x_{min}}{x_{max} - x_{min}}$

Efekt: wszystkie cechy na porównywalnej skali – szybsze uczenie, stabilne gradienty.


#WYKŁAD7 