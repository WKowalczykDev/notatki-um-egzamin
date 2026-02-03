### **1. Czyszczenie (Cleaning)**
Usuwanie „szumu” uniemożliwiającego analizę:
- **Lowercasing:** „Kot" → „kot" (unifikacja wielkości liter)
- **Usuwanie znaków specjalnych:** interpunkcja, emotikony, URL-e, znaki HTML (`<br>`, `&nbsp;`)
- **Usuwanie stop words:** „i", „ale", „w" (słowa bez znaczenia dla klasyfikacji, choć w transformerach często zostawia się je)
- **Regex/cleaning:** usunięcie nadmiarowych spacji, cyfr (jeśli nieistotne)

**Wynik:** surowy, „oczyszczony" tekst ciągły.

### **2. Tokenizacja (Tokenization)**
Podział ciągu tekstowego na **tokeny** (najmniejsze jednostiki przetwarzania):
- **Word-level:** „Ala ma kota" → [`Ala`, `ma`, `kota`]
- **Subword (BPE/WordPiece):** „tokenization" → [`token`, `##ization`] (obsługa rzadkich słów przez podział na znane fragmenty - stosowane w BERT/GPT)
- **Character-level:** litera po literze (rzadko, tylko w specyficznych zadaniach)

**Kluczowe:** To moment, w którym tekst przestaje być ciągiem znaków, a staje się **sekwencją elementów**.

### **3. Normalizacja (Normalization)**
Redukcja różnych form tego samego słowa do **wspólnej postaci bazowej** (zmniejszenie wymiarowości):
- **Stemming (obcinanie):** „pies", „psie", „psy" → „ps" (heurystyka, nie zawsze sensowna, ale szybka)
- **Lematyzacja (słownikowa):** „jestem" → „być", „szedłem" → „iść" (analiza morfologiczna, daje istniejące słowo)

**Cel:** Uniknięcie traktowania „biegnie", „biegł", „biegnijmy" jako trzech różnych, niezwiązanych ze sobą słów w modelu.

### **4. Transformacje (Transformations)**
**Najważniejszy krok:** Konwersja tekstu (słów/tokenów) na **reprezentację numeryczną** zrozumiałą dla sieci neuronowych (modele UM przyjmują tylko liczby, nie stringi).

| Rodzaj transformacji | Co robi? | Przykład | Użycie |
|---------------------|----------|----------|--------|
| **One-hot** | Wektor zer z jedną jedynką na pozycji słowa. | „kot" = `[0,0,1,0,...]` (rozmiar = wielkość słownika) | Rzadko w DL (klątwa wymiarowości), czasem w prostych ML |
| **Bag of Words (zliczanie)** | Ile razy słowo wystąpiło w dokumencie (histogram). | „krzesło": 2, „stół": 1 | Klasyfikacja dokumentów (TF-IDF) |
| **TF-IDF** | Ważona częstość (uwzględnia unikalność słowa w całym korpusie). | Słowa rzadkie dostają wyższą wagę | Wyszukiwanie informacji, klasyfikacja |
| **Zanurzenia (Embeddings)** | Gęste wektery o niskiej wymiarowości (100-300) uczące się semantyki słów (Word2Vec, GloVe) lub kontekstu (BERT) | „kot" = `[0.2, -0.5, 0.8,...]` | Input do RNN, Transformerów (najczęściej) |

**Kluczowa różnica:**
- **One-hot/BoW:** Słowa są niezależne (kot ≠ pies)
- **Embeddings:** Słowa są w relacjach (kot ≈ pies, król - mężczyzna + kobieta ≈ królowa)


### **Schemat pełny:**
`Surowy tekst` → Czyszczenie → Tokenizacja → Normalizacja → Transformacja (Embedding) → Input do sieci neuronowej
#WYKŁAD10 