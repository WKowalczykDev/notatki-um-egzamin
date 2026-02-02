### **1. Liniowa**
$$h(x) = x$$

| Zakres              | Zaleta          | Wada               | Użycie                                                           |
| ------------------- | --------------- | ------------------ | ---------------------------------------------------------------- |
| $(-\infty, \infty)$ | Zachowuje skalę | Brak nieliniowości | **Tylko wyjście** przy regresji (przewidywanie wartości ciągłej) |

**Egzamin:** Jeśli użyjesz w warstwach ukrytych, cała sieć redukuje się do jednej warstwy liniowej.

---

### **2. Sigmoid**
$$h(x) = \frac{1}{1 + e^{-x}}$$

| Zakres | Zaleta | Wada | Użycie |
|--------|--------|------|--------|
| $(0, 1)$ | Wyjście = prawdopodobieństwo | **Vanishing gradient** (dla $|x|>5$ gradient $\approx 0$) | Warstwa **wyjściowa** w klasyfikacji **binarnej** |

**Egzamin:** Nie używaj w głębokich warstwach ukrytych – sieć "zamarza" (brak uczenia).

---

### **3. Tanh (tangens hiperboliczny)**
$$h(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$

| Zakres | Zaleta | Wada | Użycie |
|--------|--------|------|--------|
| $(-1, 1)$ | **Zero-centered** (średnia $\approx 0$, lepsza niż sigmoid) | Też **vanishing gradient** | Warstwy **ukryte** w RNN/LSTM (starsze architektury) |

**Egzamin:** Lepszy niż sigmoid dla ukrytych warstw, bo ujemne wartości "tłumią" niepożądane cechy.

---

### **4. ReLU (Rectified Linear Unit)**
$$h(x) = \begin{cases} x & \text{dla } x \geq 0 \\ 0 & \text{dla } x < 0 \end{cases}$$

| Zakres | Zaleta | Wada | Użycie |
|--------|--------|------|--------|
| $[0, \infty)$ | Szybka, brak zanikania gradientu dla $x>0$ | **Dying ReLU** (neuron "umiera" gdy ciągle $x<0$) | **Domyślna** dla warstw ukrytych w CNN/MLP |

**Egzamin:** Najpopularniejsza obecnie. Leczenie Dying ReLU: Leaky ReLU (dla $x<0$ daje np. $0.01x$).

---

### **5. Swish**
$$h(x) = x \cdot \sigma(x) = \frac{x}{1 + e^{-x}}$$

| Zakres | Zaleta | Wada | Użycie |
|--------|--------|------|--------|
| $(-\infty, \infty)$ (gładka) | Nie "umiera" dla $x<0$ (małe ujemne wartości), gładka | Wolniejsza (trzeba liczyć $\exp$) | Nowoczesne sieci (EfficientNet), gdy liczy się dokładność |

**Egzamin:** "Gładki ReLU" – zachowuje się jak ReLU dla dodatnich, ale nie ucina całkowicie ujemnych.

---

### **6. Softmax**
$$h(z_i) = \frac{e^{z_i}}{\sum_{j=1}^{k} e^{z_j}} \quad \text{dla wektora } z = [z_1, ..., z_k]$$

| Zakres | Zaleta | Wada | Użycie |
|--------|--------|------|--------|
| $(0, 1)$ dla każdej klasy, $\sum = 1$ | Rozkład prawdopodobieństwa sumujący się do 1 | Ekstremalne wartości $e^{z_i}$ mogą "wybuchnąć" (trzeba stabilizować) | Warstwa **wyjściowa** w klasyfikacji **wieloklasowej** (>2 klasy) |

**Egzamin:** Przyjmuje **wektor** logitów, zwraca wektor prawdopodobieństw. Wybierasz klasę z $\max(softmax)$.

---

**Ściąga wyboru funkcji:**
- **Warstwa ukryta:** ReLU (standard) lub Swish (nowoczesne)
- **Wyjście binarne (2 klasy):** Sigmoid
- **Wyjście wieloklasowe (k klas):** Softmax  
- **Wyjście regresja:** Liniowa
#WYKŁAD7 