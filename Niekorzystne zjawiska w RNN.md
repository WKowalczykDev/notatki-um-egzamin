## Głównym problemem w RNN jest Vanishing & Exploding Gradients

### **1. Przyczyna matematyczna (dlaczego to się dzieje?)**

W RNN ta sama macierz wag **W** jest mnożona przez siebie wielokrotnie wzdłuż czasu (przy propagacji wstecznej BPTT).

Rozkład spektralny (eigendecomposition):
$$W = V \cdot \text{diag}(\lambda) \cdot V^{-1}$$

Po $t$ krokach czasowych:
$$W^t = V \cdot \text{diag}(\lambda)^t \cdot V^{-1} = V \cdot \begin{bmatrix} \lambda_1^t & 0 & \dots \\ 0 & \lambda_2^t & \dots \\ \vdots & \vdots & \ddots \end{bmatrix} \cdot V^{-1}$$

**Interpretacja:**
- Jeśli $|\lambda| < 1$ (wartości własne < 1): $\lambda^t \to 0$ przy dużym $t$ → **zanikanie gradientu**
- Jeśli $|\lambda| > 1$: $\lambda^t \to \infty$ → **eksplozja gradientu**
- Efekt jest **wykładniczy** względem długości sekwencji.

### **2. Zanikający gradient (Vanishing Gradient)**

**Objawy:**
- Sieć ma **krótką pamięć** (short-term memory) – „pamięta” tylko ostatnie 5-10 kroków, wcześniejsze są zapomniane.
- Wagi na początku sekwencji prawie się nie zmieniają (brak uczenia długoterminowych zależności).
### **3. Eksplodujący gradient (Exploding Gradient)**

**Objawy:**
- Wagi „wariują” podczas uczenia (skaczą do NaN lub ogromnych wartości).
- Utrata stabilności – sieć nie zbiega.

### **4. LSTM jako rozwiązanie architektoniczne (Long Short-Term Memory)**

Zamiast prostej komórki RNN, LSTM wprowadza **komórkę pamięci (cell state, c)** przepływającą przez całą sekwencję z minimalnymi zmianami (liniowa „autostrada”), oraz trzy **bramki (gates)** kontrolujące przepływ informacji:

| Bramka | Funkcja | Równanie (uproszczone) |
|--------|---------|------------------------|
| **Forget gate (f)** | Decyduje, co usunąć z pamięci | $\sigma(W_f \cdot [h_{t-1}, x_t] + b_f)$ |
| **Input gate (i)** | Decyduje, co dodać do pamięci | $\sigma(W_i \cdot [h_{t-1}, x_t] + b_i)$ |
| **Output gate (o)** | Decyduje, co wypuścić na wyjście | $\sigma(W_o \cdot [h_{t-1}, x_t] + b_o)$ |

**Mechanizm działania:**
1. **Cell state (c)** przepływa prawie bez zmian (suma, mnożenie) – gradient może „przepłynąć” przez 100 kroków bez zanikania.
2. **Hidden state (h)** to „filtrowana” wersja cell state (przepuszczona przez tanh i bramkę output).
3. **Intelligent forgetting**: Sieć uczy się, które informacje są ważne (zapamiętać) a które śmieci (wyrzucić).

**GRU (Gated Recurrent Unit):** Uproszczona wersja LSTM (tylko 2 bramki: reset i update), często podobna skuteczność, mniej parametrów.

---

### **Podsumowanie**

- **RNN klasyczne** cierpią na brak pamięci długoterminowej przez mnożenie macierzy wag (wartości własne < 1 → zanikanie, > 1 → eksplozja).
- **Vanishing**: Gradienty zanikają w czasie → krótka pamięć. Leczenie: ReLU, LSTM/GRU.
- **Exploding**: Gradienty wybuchają → niestabilność. Leczenie: Gradient clipping, truncated BPTT.
- **LSTM** rozwiązuje problem przez **cell state** (szyna dla gradientu) i **bramki** (kontrola zapominania/pamiętania).

#WYKŁAD8 