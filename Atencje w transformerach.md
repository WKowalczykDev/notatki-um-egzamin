### **1. Definicja Atencji (Attention Mechanism)**
Mechanizm pozwalający modelowi **dynamicznie ważyć znaczenie** (ważność) każdego tokenu w sekwencji względem każdego innego tokenu, tworząc **kontekstową reprezentację** zależną od całego otoczenia.

W przeciwieństwie do RNN (gdzie informacja musi przepływać krok po kroku), atencja pozwala na **bezpośrednie połączenie** (shortcut) między dowolnymi pozycjami w sekwencji, eliminując problem „dystansu" (vanishing gradient przy długich sekwencjach).
### **2. Samoatencja (Self-Attention)**
Każdy token „patrzy" na wszystkie inne tokeny w **tej samej sekwencji** (stąd „self"), aby zrozumieć swoje znaczenie w kontekście.

**Mechanizm działania:**
- Token tworzy trzy wektory: **Query (Q)** – „czego szukam?", **Key (K)** – „co oferuję?", **Value (V)** – „jaką informację niosę?"
- Obliczana jest **macierz podobieństwa** $Q \times K^T$ (skalarne podobieństwo zapytań do kluczy).
- Wynik normalizowany (Softmax) tworzy wagi atencji.
- **Wzmocnienie:** Wysoka waga (bliska 1) dla tokenów semantycznie powiązanych (np. zaimków i ich poprzedników).
- **Osłabienie:** Niska waga (bliska 0) dla nieistotnych tokenów (przymków, przecinków w danym kontekście).

**Efekt:** Każdy token na wyjściu jest **ważoną sumą** wszystkich tokenów wejściowych, gdzie wagi zależą od semantycznej relacji.

### **3. Atencja Wielogłowicowa (Multi-Head Attention)**
Zamiast jednego „spojrzenia" na relacje, model używa **wielu głów (heads)** równolegle (np. 8, 16).

**Idea:** Różne „głowy" specjalizują się w wykrywaniu różnych typów zależności:
- **Głowa 1:** Relacje podmiot-orzeczenie.
- **Głowa 2:** Zaimki wskazujące (referencje).
- **Głowa 3:** Zależności czasowe (przed/po).
- **Głowa N:** Relacje składniowe, semantyczne, itp.

**Łączenie:** Wyniki wszystkich głów są konkatenowane (sklejane) i przepuszczane przez warstwę liniową, tworząc bogatą, wieloaspektową reprezentację.

### **4. Rodzaje Atencji w Architekturze**

#### **W Koderze (Encoder Self-Attention):**
- **Bidirectional (dwukierunkowa):** Token może patrzeć na **wszystkie** inne tokeny (zarówno wcześniejsze, jak i późniejsze).
- Cel: Pełne zrozumienie kontekstu zdania (jak w BERT).

#### **W Dekoderze (Masked Self-Attention):**
- **Autoregresyjna:** Token może patrzeć tylko na **wcześniejsze** tokeny (maska blokuje dostęp do przyszłych pozycji).
- Cel: Podczas generowania tekstu nie można „ściągać" z przyszłych słów, których jeszcze nie wygenerowano (jak w GPT).

#### **Cross-Attention (Encoder-Decoder):**
- Query pochodzi z dekodera (aktualny stan generowania), Key i Value z wyjścia ostatniego kodera (przetworzone źródło).
- Cel: Tłumaczenie maszynowe – dekoder „zwraca uwagę" na odpowiednie fragmenty oryginału podczas generowania tłumaczenia.

### **5. Zalety Mechanizmu Atencji**
- **Długie zależności:** Token na pozycji 1000 może bezpośrednio „zobaczyć" token na pozycji 1 (brak zanikania).
- **Równoległość:** Wszystkie pozycje przetwarzane jednocześnie (w przeciwieństwie do sekwencyjnego RNN).
- **Interpretowalność:** Macierz atencji pokazuje, które słowa model uznał za istotne dla siebie (wizualizacja „mapy ciepła").

---

### **Powrót do architektury:**
Szczegóły o rozmieszczeniu atencji w blokach koderów/dekoderów oraz kaskadowym stosowaniu → zobacz główną notatkę: [[Transformery]]
#WYKŁAD10 