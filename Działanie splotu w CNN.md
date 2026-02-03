### **1. Definicja podstawowa**
Splot to przesuwanie **jądra (kernela)** — małej macierzy wag (np. 3×3) — po całym obrazie (wejściowej mapie cech).
- **Operacja:** Iloczyn skalarny (element-wise multiplication + suma) między fragmentem obrazu a jądrem.
- **Wynik:** Pojedyncza liczba w **mapie cech (feature map)**.
- **Intuicja:** Jeśli fragment obrazu „pasuje” do wzorca zapisnego w jądrze (wysoki iloczyn skalarny), mapa cech ma wysoką wartość.

### **2. Kluczowa właściwość: FIR (Finite Impulse Response)**
- **Jądro ma skończony rozmiar** (np. 3×3, 5×5, nigdy „nieskończone”).
- **Konsekwencja:** Wpływ pojedynczego piksela wejściowego (impulsu) na wyjście jest **lokalny i ograniczony**.
- **Odpowiedź impulsowa:** Jeśli wstawisz 1 w jednym miejscu inputu, to po splicie aktywacja pojawi się tylko w małym oknie (rozmiar jądra), reszta to zera.
- **Dlaczego to ważne:** Wiadomo dokładnie, ile warstw potrzeba, aby „zobaczyć” cały obraz (głębokość × rozmiar jądra).

### **3. Lokalne pole recepcyjne vs. Hierarchia**
- **Pojedynczy splot:** Neuron „widzi” tylko 3×3 pikseli (lokalnie).
- **Wiele splotów (głębokość):** Stosując warstwę po warstwie, pole recepcyjne rośnie:
  - Warstwa 1: 3×3 (**krawędzie**) - przekazujemy mapę krawędzi niżej
  - Warstwa 2: 5×5 (**tekstury z krawędzi**) - na podstawie mapy krawędzi
  - Warstwa 3: 7×7 (**części obiektów**) - na podstawie mapy tekstur
  - ... bez użycia ogromnych, nieefektywnych filtrów na wejściu.
- **Efekt:** Nauka cech hierarchicznych przy niewielkiej liczbie parametrów (współdzielenie wag).

### **5. Stabilność: Brak sprzężenia zwrotnego (vs. RNN)**
- **CNN (FIR):** Struktura **feedforward** (tylko w przód). Nie ma pętli zwrotnej (rekurencji).
- **RNN (IIR):** Ma pętlę (stan przekazywany do siebie), co może powodować nieskończoną odpowiedź impulsową (exploding/vanishing gradients).
- **Wniosek:** Splot w CNN jest matematycznie **stabilny** — nie wybucha i nie zanika w nieskończoność przez samą strukturę (chociaż vanishing gradients w głębokich sieciach mogą wystąpić z innych powodów, stąd ReLU).

### **Podsumowanie**
1. Splot = **lokalny filtr** (jądro) przesuwany po obrazie.
2. Jest to system **FIR** (skończona odpowiedź impulsowa) — wpływ ograniczony rozmiarem kernela.
3. Działa jak **detektor podobieństwa** — wysoka aktywacja = wzorzec pasuje do fragmentu obrazu.
4. **Brak sprzężenia zwrotnego** — stabilniejsze niż RNN, hierarchia budowana przez stosowanie wielu warstw splotowych.

### Parametry filtrów są uczone:
  • dzięki zastosowaniu współdzielenia wag sieci CNN są prostsze niż MLP o tym samym zastosowaniu, ale...
  • w praktyce do skomplikowanych zastosowań używamy CNN o ogromnej liczbie wag — ich efektywne wyuczenie zajmuje dużo czasu, dlatego w praktyce używamy sieci CNN już wstępnie wytrenowanych (uczenie transferowe).


#WYKŁAD8 