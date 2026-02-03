### **1. Kodowanie Pozycyjne (Positional Encoding)**
**Problem:** Atencja sama w sobie jest **permutacyjna** (niezmiennicza względem kolejności). Dla modelu „kot je mysz" = „mysz je kot" (te same tokeny, inna kolejność).
**Rozwiązanie:** Dodanie informacji o pozycji tokenu w zdaniu do embeddingu wejściowego.
- **Implementacja:** Sinusoidalne funkcje (sin/cos) o różnych częstotliwościach lub nauczone embeddingi pozycyjne.
- **Efekt:** Model „wie", czy słowo jest na początku (pozycja 0), środku (50), czy końcu (500) zdania. Bez tego nie ma pojęcia o składni (podmiot przed orzeczeniem).
### **2. Połączenia Rezydualne (Residual Connections / Skip Connections)**
**Mechanizm:** Strzałka omijająca blok (zobacz „Add & Norm" na schemacie) – wejście bloku jest dodawane do jego wyjścia (przed normalizacją).
- **Dla atencji:** $X + \text{Attention}(X)$
- **Dla FFN:** $X + \text{FFN}(X)$
**Dlaczego?** Ułatwiają przepływ gradientu w głębokich sieciach (12-24 warstwy). Zapobiegają „zanikaniu" informacji – oryginalny sygnał zawsze ma „skrót" do wyjścia. To kluczowe dla treningu głębokich modeli (bez tego byłyby niestabilne).
### **3. Normalizacja Warstwowa (Layer Normalization)**
**„Norm" w „Add & Norm":** Normalizacja przeprowadzana **wzdłuż wymiaru cech** (dla każdego tokenu osobno), nie wzdłuż batcha (jak w BatchNorm).
- **Działanie:** Skalowanie i przesunięcie aktywacji tak, by miały średnią 0 i wariancję 1.
- **Cel:** Stabilizacja treningu – zapobiega „wariactwu" wartości w głębokich warstwach (eksplodującym/zanikającym aktywacjom). Umożliwia użycie wyższych learning rates
### **4. Warstwy Feed-Forward (FFN / MLP)**
**Po atencji następuje:** Prosta sieć MLP (zazwyczaj 2 warstwy: rozszerzenie 4x i zwrot do wymiaru modelu, np. 512 → 2048 → 512) z funkcją aktywacji ReLU/GELU.
- **Działanie:** Stosowana **niezależnie** do każdej pozycji (point-wise), bez mieszania informacji między tokenami (to robi atencja).
- **Rola:** Wprowadzenie **nieliniowości** i przetworzenie reprezentacji po atencji (tak jak w klasycznych MLP). Atencja „zbiera" informację z kontekstu, FFN „przetwarza" ją lokalnie.
### **5. Maskowanie w Dekoderach (Look-ahead Mask)**
**Masked Multi-Head Attention:** W dekoderze (prawa strona schematu) stosowana jest maska (zazwyczaj trójkątna, dolnotrójkątna), która **blokuje dostęp do przyszłych tokenów**.
- **Dlaczego?** Podczas generowania tekstu (np. tłumaczenia) model nie może „ściągać" z przyszłych słów, których jeszcze nie wygenerował. Może patrzeć tylko na wcześniejsze pozycje (0 do t-1), nie na t+1.
- **Implementacja:** Ustawienie wartości atencji na $-\infty$ (po softmax = 0) dla „przyszłych" pozycji.
### **6. Generowanie Wyjścia (Softmax na końcu)**
**Warstwa Linear + Softmax:**
- **Linear:** Projekcja ostatniego stanu ukrytego dekodera na wymiar słownika (vocab size, np. 30 000 tokenów).
- **Softmax:** Zamiana logitów na rozkład prawdopodobieństwa (suma = 1).
- **Przewidywanie:** Model wybiera token o najwyższym prawdopodobieństwie (lub próbkuje z rozkładu dla kreatywności).

**Uwaga:** W dekoderze generowanie jest **autoregresyjne** – wyprodukowany token staje się wejściem dla następnego kroku (stąd „Outputs (shifted right)" na schemacie – przesunięcie o jeden w prawo, by nie patrzeć na przyszłość).

#WYKŁAD10 