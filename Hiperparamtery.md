**Hiperparametry** - ustawienia **przed** treningiem definiujące jak sieć się ucz i z czego się składa

### **1. Proces uczenia i kontrola bias/variance**
Te parametry decydują **jak szybko i dokładnie** sieć się uczy oraz jak bardzo unika przeuczenia (overfittingu).

| Hiperparametr | Co kontroluje? |
|---------------|----------------|
| **Learning rate** | Wielkość kroku w gradient descent (za duży – przestrzelisz minimum, za mały – uczysz się wieki). |
| **Batch size** | Ile próbek naraz przetwarzasz przed aktualizacją wag (mały = więcej szumu/regularizacji, duży = stabilniejszy gradient). |
| **Epochs** | Ile razy cały zbiór treningowy przechodzi przez sieć (za mało – underfitting, za dużo – overfitting). |
| **Regularization rate** (lambda) | Siła kary za duże wagi (L1/L2) – im wyższa, tym bardziej „wymuszona” prostota modelu. |
| **Dropout** | Prawdopodobieństwo wyłączenia neuronu podczas treningu (np. 0.2 = 20% neuronów „śpi”). |

**Cel:** Znalezienie balansu między dopasowaniem do danych (low bias) a generalizacją (low variance).

### **2. Algorytm**
Te parametry definiują **matematyczne podstawy** uczenia – jak obliczamy błąd i jak reagujemy na niego.

| Hiperparametr | Co wybierasz? |
|---------------|---------------|
| **Cost function** | Funkcja kosztu (jak mierzymy błąd): MSE (regresja), Cross-Entropy (klasyfikacja). |
| **Optimizer** | Algorytm aktualizacji wag: Adam (domyślny), SGD, RMSprop. |
| **Activation functions** | Funkcje aktywacji neuronów: ReLU (warstwy ukryte), Sigmoid/Softmax (wyjście). |

**Cel:** Zapewnienie efektywnego i stabilnego procesu optymalizacji (np. Adam szybciej zbiega niż SGD, nie zatrzymuje sie w lokalnym minimum).

### **3. Architektura sieci**
Te parametry definiują **strukturę** (kształt) sieci – jak jest zbudowana fizycznie.

| Hiperparametr | Co kontroluje? |
|---------------|----------------|
| **Number of layers** | Głębokość sieci (ile warstw ukrytych). |
| **Number of neurons** | Szerokość warstw (ile neuronów w każdej warstwie). |
| **Filter dimensions** (CNN) | Rozmiar filtra splotowego (np. 3×3, 5×5). |
| **Stride** (CNN) | Krok przesunięcia filtra (1 = dokładny, 2 = szybszy, mniejszy wynik). |
| **Padding** (CNN) | Dopełnienie zerami na brzegach obrazu (valid = bez, same = zachowaj rozmiar). |
| **Pooling type/size** (CNN) | Rodzaj downsamplingu (MaxPool = bierz max, AveragePool = średnia) i jego rozmiar. |

**Cel:** Określenie pojemności modelu (ile może się nauczyć) i sposobu ekstrakcji cech (szczególnie w CNN).

---

### **Kluczowa różnica (egzamin):**
- **Hiperparametry** (z powyższych 3 kategorii) – wybierasz ręcznie (tuning, grid search, walidacja).
- **Parametry** (wagi $W$ i biasy $b$) – sieć uczy się sama podczas treningu (backpropagation).

#WYKŁAD9 