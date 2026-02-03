### MLP (Multi-Layer Perceptron) — „Klasyczna” sieć w pełni połączona

**Czym jest:**  
Sieć, gdzie każdy neuron warstwy i jest połączony z **każdym** neuronem warstwy i+1 (fully connected). To, co opisywaliśmy wcześniej jako „standardową sieć”.

**Problem z obrazami (dlaczego MLP nie nadaje się do zdjęć):**
- **Klątwa wymiarowości:** Obraz 1000×1000 pikseli (RGB) to 3 miliony wejść. Jeśli pierwsza warstwa ukryta ma 1000 neuronów, masz 3000000×1000=3 miliardy wag **w jednej warstwie**. To niemożliwe do nauczenia.
- **Brak struktury przestrzennej:** MLP wymaga spłaszczenia obrazu do wektora (1D). Tracisz informację, które piksele są obok siebie (sąsiedztwo). Dla MLP piksel (1,1) i (100,100) są tak samo oddalone jak (1,1) i (1,2).

**Użycie MLP:**  
Dane tabelaryczne (np. ceny mieszkań, parametry pacjenta), gdzie kolejność cech nie ma znaczenia, lub jako **ostatnia część** CNN (klasyfikacja).



#WYKŁAD8 