**Transformery – Architektura i Funkcjonalności**

---

### 1. Dlaczego transformery powstały (paradygmat)
Rezygnacja z rekurencji (RNN) na rzecz **przetwarzania całej sekwencji jednocześnie** (non-sequential). Rozwiązuje to problem zanikania gradientu i krótkiej pamięci charakterystyczny dla sieci rekurencyjnych, umożliwiając pełne wykorzystanie GPU (równoległość).
### **2. Struktura Wejściowa**
Zamiast przetwarzać słowa krok po kroku, Transformer przyjmuje całe zdanie naraz, ale wymaga sztucznego wprowadzenia informacji o kolejności:
- **Embeddingi tokenów:** Gęste wektory słów (jak w Word2Vec).
- **Kodowanie Pozycyjne (Positional Encoding):** Dodawane do embeddingów, by model „wiedział”, czy słowo „kot” jest na początku czy końcu zdania (brak RNN = brak wbudowanej kolejności).
### **3. Bloki Koderów (Encoders) – Zrozumienie**
Stos (stack) identycznych warstw (np. 6, 12 lub 24).
- **Zadanie:** Stworzenie głębokiej, kontekstowej reprezentacji każdego tokenu (wektorów uwzględniających całe otoczenie).
- **Składniki warstwy:**
  - [[Atencje w transformerach|Mechanizm atencji (Self-Attention)]] – filtrowanie i ważenie relacji między tokenami.
  - **Sieć Feed-Forward (FFN):** Prosta sieć MLP stosowana niezaleśnie do każdej pozycji (point-wise), przekształcająca reprezentacje po atencji.
  - **Add & Norm:** Połączenia rezydualne (skip connections) + normalizacja warstw – kluczowe dla stabilnego uczenia głębokich modeli (przepływ gradientu).
### **4. Bloki Dekoderów (Decoders) – Generowanie**
Stos warstw (analogiczny do kodera, ale z modyfikacjami).
- **Zadanie:** Generowanie sekwencji wyjściowej token po tokenie (autoregresyjnie).
- **Składniki warstwy:**
  - Masked [[Atencje w transformerach|Self-Attention]] – atencja „w przód" jest zablokowana (może patrzeć tylko na wcześniejsze tokeny wygenerowanego tekstu).
  - **Cross-Attention (Encoder-Decoder Attention):** Warstwa łącząca dekoder z wyjściem ostatniego kodera (umożliwia tłumaczenie: dekoder „patrzy" na oryginalne zdanie).
  - FFN + Add & Norm (jak w kodrze).
### **5. Kaskadowe Łączenie (Stacking Nx)**
Warstwy są układane szeregowo (np. 6 koderów, potem 6 dekoderów). Każda kolejna warstwa **refinuje** reprezentację, budując hierarchię abstrakcji podobnie jak w CNN – niższe warstwy widzą lokalne zależności, wyższe globalne struktury zdaniowe.

### **6. Warianty Architektoniczne (Zastosowania)**
W zależności od zadania, używa się różnych części Transformerów:

| Wariant | Struktura | Zadanie | Przykład |
|---------|-----------|---------|----------|
| **Encoder-only** | Tylko stos koderów | Rozumienie języka (klasyfikacja, NER, pytania-odpowiedzi) | **BERT** |
| **Decoder-only** | Tylko stos dekoderów | Generowanie tekstu (autoregresywne) | **GPT, ChatGPT** |
| **Encoder-Decoder** | Pełna architektura | Tłumaczenie maszynowe, podsumowanie tekstu | **T5, oryginalny Transformer** |



#WYKŁAD10 