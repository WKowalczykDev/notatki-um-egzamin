## Sieci rekurencyjne RNN - _ang. recurrent neutral networks_
RNN to ta sama sieć neuronowa uruchamiana w pętli, gdzie wyjście z poprzedniego kroku (stan pamięci) staje się wejściem do następnego. Pozwala to modelować zależności czasowe i kontekstowe w danych.

Używana jest do analizy szeregów czasowych -np. kursu dolara

---
### **1. Problem: Dlaczego MLP nie wystarcza?**
Zwykła sieć neuronowa (MLP, CNN) zakłada, że każda próbka jest **niezależna**. Jeśli masz zdanie „Kot je mysz”, MLP widzi trzy osobne słowa lub jeden wielki wektor, ale **nie rozumie kolejności** („mysz je kot” wygląda dla niej tak samo). Brakuje jej **pamięti czasowej**.

### **2. Rozwiązanie RNN: Jedna komórka, wiele kroków czasowych**
RNN nie przetwarza całej sekwencji naraz. Robi to **krok po kroku** (sequentially), używając tej samej sieci (komórki) wielokrotnie.

**Mechanizm (slajd 1 - „Context Units”):**
W każdym kroku czasowym $t$ komórka dostaje:
1.  **Aktualne dane wejściowe** $x_t$ (np. litera „B” lub słowo „Kot”).
2.  **Stan wewnętrzny / ukryty** $h_{t-1}$ (ang. *hidden state*, na slajdzie „Context Units”) – to jest **pamięć** zawierająca skompresowaną informację o wszystkim, co sieć widziała wcześniej (kontekst).

**Co produkuje:**
- **Wyjście** $y_t$ (np. predykcja następnego słowa).
- **Nowy stan ukryty** $h_t$ – aktualizowana pamięć, która leci do następnego kroku (strzałka zwrotna *feedback*).

**Kluczowe:** To jest **ta sama komórka** (te same wagi!) uruchamiana w pętli. Nie masz osobnej sieci dla słowa „Kot” i osobnej dla „je”. Masz jedną sieć, która „przesuwa się” w czasie.

### **3. Uczenie kontekstowe (Context Learning)**
Dzięki sprzężeniu zwrotnemu (przekazywaniu $h_t$ dalej), wyjście w kroku 2 („je”) zależy nie tylko od słowa „je”, ale też od stanu $h_1$, który pamięta „Kot”. Dlatego sieć wie, że to **kot je**, a nie mysz je. To się nazywa **uczenie kontekstowe**.

---

### **4. Kluczowe właściwości**

| Cecha | Co to oznacza? | Dlaczego to ważne? |
|-------|----------------|--------------------|
| **Dane sekwencyjne** | Kolejność ma znaczenie (czasowa zależność). | „Alice loves Bob” $\neq$ „Bob loves Alice”. |
| **Różna długość** (Variable Length) | Ta sama sieć obsługuje krótkie (5 słów) i długie (500 słów) sekwencje. | Nie musisz zmieniać architektury dla różnych długości zdań. |
| **Nie losujemy w paczce!** (No shuffling) | Próbek w batchu nie można mieszać losowo. | Krok 5 potrzebuje pamięci z kroku 4. Losowa kolejność zniszczy sens. |
| **Skalowalność** | Parametry rosną względem rozmiaru komórki, nie długości sekwencji. | W przeciwieństwie do „SSN” (stare podejście: spłaszczanie sekwencji do jednego długiego wektora), RNN unika klątwy wymiarowości. |

---

### **5. Intuicja: RNN jako pętla for**
Wyobraź sobie kod:

```python
h = 0  # Początkowa pamięć (Context Unit)
for x in sequence:  # Dla każdego kroku czasowego
    y, h = cell(x, h)  # Ta sama komórka, aktualizacja pamięci
    output.append(y)
```

**W MLP** musiałbyś mieć osobne zmienne `x1, x2, x3...` i osobne warstwy dla każdego kroku. **W RNN** masz jedną zmienną `h`, która „nosi” informację przez całą pętlę.

---

### **Podsumowanie**
RNN to sieć ze **sprzężeniem zwrotnym w czasie**, która przetwarza dane sekwencyjnie (krok po kroku), zachowując **stan wewnętrzny (Context Units)** między krokami. Dzięki temu rozumie kontekst i może obsługiwać sekwencje zmiennej długości bez zmiany architektury. Nie wolno mieszać kolejności próbek w batchu, bo zależność czasowa jest kluczowa.


![[Pasted image 20260203114609.png]]
#WYKŁAD8 