Nastąpił koniec ery, w której dominowały RNN/LSTM, i początek ery **Transformerów** (jak BERT, GPT).

W skrócie: zamiast czytać tekst **słowo po słowie** (rekurencyjnie), modele patrzą na **całe zdanie naraz** i rysują połączenia między słowami, które są istotne.

---

### **1. Problem z RNN (dlaczego odchodzimy)**

RNN (w tym LSTM) działają jak człowiek czytający książkę:
- Czytasz wyraz 1, zapamiętujesz w głowie (stan ukryty).
- Czytasz wyraz 2, aktualizujesz pamięć.
- ...
- Żeby zrozumieć wyraz 100, musisz przejść przez poprzednie 99.

**Wady:**
- **Wolne:** Nie możesz przyspieszyć, bo krok 100 wymaga wyniku z 99 (sekwencyjność). Trudno wykorzystać pełną moc GPU (które lubią równoległe obliczenia).
- **Słaba pamięć:** Jeśli słowo na początku zdania (wyraz 1) jest kluczowe dla znaczenia wyrazu 500, gradient musi przejść przez 499 kroków (BPTT) — zanika lub wybucha.

---

### **2. Czym jest Atencja (Attention)?**

Zamiast polegać na skompresowanej „pamięci” (ukrytym stanie $h$), model używa **mechanizmu uwagi**:
- Gdy produkuje wyjście (np. tłumaczy słowo), patrzy na **wszystkie** słowa wejściowe jednocześnie.
- Przypisuje im **wagi** (np. „to słowo jest ważne = 0.8, to nieistotne = 0.01”).
- Działa jak **latarka** — skupia się na konkretnych fragmentach tekstu, które są aktualnie potrzebne.

**Przykład (tłumaczenie):**
Zdanie: „The cat sat on the mat because **it** was tired.”
Tłumacząc „it”, model z **atencją** patrzy wstecz i „świeci latarką” na słowo „cat” (a nie „mat”), bo to kot był zmęczony, nie dywan.

---

### **3. Self-Attention (Uwaga własna) — kluczowa innowacja**

W Transformersach (BERT, GPT) używa się **Self-Attention**:
- Model nie patrzy tylko z wejścia na wyjście (jak w starych Seq2Seq), ale **każde słowo patrzy na każde inne słowo w tym samym zdaniu**.
- Tworzy się **pełna sieć połączeń** (graf): słowo 1 „rozmawia” ze słowem 500 bezpośrednio, w jednym kroku.

**Efekt:**
- Słowo „bank” w „river bank” dostaje inny kontekst niż „bank” w „bank account”, bo patrzy na sąsiadów („river” vs „money”) i na tej podstawie modyfikuje swoje znaczenie (embedding).

---

### **4. Transformer (architektura bez rekurencji)**

Nowe modele (BERT, GPT-4, T5) składają się wyłącznie z:
1.  **Warstw Self-Attention** (patrzenie na siebie nawzajem).
2.  **Warstw Feed-Forward** (zwykłe sieci neuronowe, bez pętli czasowych).
3.  **Brak RNN:** Nie ma „komórek” przekazujących stan w czasie. Nie ma $h_t$ zależnego od $h_{t-1}$.

**Zalety:**
- **Równoległość:** Wszystkie słowa w zdaniu są przetwarzane **jednocześnie** (można wrzucić na GPU i obliczyć wszystko naraz). Trening jest 10x-100x szybszy niż LSTM.
- **Długie zależności:** Słowo 1 może bezpośrednio „porozmawiać” ze słowem 500 bez zanikania gradientu (bo jest bezpośrednie połączenie przez mechanizm uwagi, nie przez łańcuch 500 macierzy).

---

### **Podsumowanie dla egzaminu**

| Cecha | Stare RNN/LSTM | Nowe Transformery (Attention) |
|-------|----------------|-------------------------------|
| **Przetwarzanie** | Sekwencyjne (krok po kroku) | Równoległe (wszystko naraz) |
| **Pamięć** | Ukryty stan $h$ (skompresowany) | Bezpośrednie połączenia (Self-Attention) |
| **Długie zdania** | Problem (vanishing gradient) | Brak problemu (dystans = 1 krok) |
| **Przykłady** | Stare systemy tłumaczenia | **BERT** (Google), **GPT** (OpenAI), **T5** |

**„Odchodzi się od rekurencji”** = rezygnujemy z pętli czasowej (RNN) na rzecz „patrzenia na wszystko naraz” (Attention), co jest szybsze i lepsze w łapaniu kontekstu.

#WYKŁAD8 