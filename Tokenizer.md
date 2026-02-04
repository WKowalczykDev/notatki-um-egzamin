**Tokenizacja w LLM – Notatka Podsumowująca**

---

### **1. Kluczowe Pojęcia: Vocabulary vs Embedding**

Gdy model ma **„128k tokenów"** i **„rozmiar embeddingu 4096"**:

- **128k tokens** (słownik/vocabulary): To liczba unikalnych „słów" (tokenów), które model rozpoznaje. Każdy token ma przypisany indeks (0 do 127 999). To rozmiar przestrzeni dyskretnej (jak one-hot, ale gęsty).
- **4096** (wymiar embeddingu): To **długość wektora** (tak, wymiar wektora liczb zmiennoprzecinkowych), który reprezentuje każdy token. Każdy z 128k tokenów ma swój unikalny wektor o długości 4096. To determinuje pojemność reprezentacyjną (ile informacji może „zmieścić" się w pojedynczym tokenie).

**Analogia:** Słownik ma 128 000 haseł, ale każde hasło opisane jest 4096 cechami (wymiarami).

---

### **2. Byte Pair Encoding (BPE) – Mechanizm Działania**

BPE to **tokenizacja subwordowa** (między poziomem znaku a słowem). Rozwiązuje problem ograniczonego słownika (jak obsłużyć rzadkie słowa lub nowe słowa?).

**Algorytm treningu (jak na slajdzie ze „unrelated"):**
1. **Start:** Tekst podzielony na pojedyncze znaki (bajty UTF-8): `u-n-r-e-l-a-t-e-d`
2. **Iteracja:** Znajdź najczęściej występujące **sąsiednie pary** znaków (np. `e-d`), połącz je w nowy token (`ed`).
3. **Powtarzaj:** Kontynuuj łączenie (`at` → `ated` → `lated` → `related` → `un-related` → `unrelated`).
4. **Wynik:** Słownik zawiera zarówno pojedyncze litery, jak i częste sylaby, morfemy i całe słowa.

**Dlaczego to działa?**
- **Rzadkie słowa:** „Szczęście" może zostać podzielone na znane podjednostki (`Szczę` + `ście`), jeśli całe słowo nie było w treningu.
- **Kod:** Języki programowania (Python) mają regularną składnię – BPE uczy się tokenów jak `num_`, `sqrt`, ` = `, `print(`, co jest efektywne.
- **Wielojęzyczność:** Działa na poziomie bajtów UTF-8 – obsługuje chińskie znaki, polskie „ł/ą", emoji bez specjalnych reguł (zmienną długość bajtową).

**Tiktoken:** Produkcyjna implementacja BPE używana przez OpenAI, zoptymalizowana pod wydajność (C++), z heurystykami i ręcznie dodanymi specjalnymi tokenami (jak `<|endoftext|>`).

---

### **3. Specyfika Tokenizerów LLM (Llama, GPT)**

**Tokenizera to część modelu** – jest powiązana z konkretnym modelem i trenowana osobno:
- **Proporcje językowe:** Jeśli trening to 90% angielski i 10% kod Python, tokenizer będzie miał więcej efektywnych tokenów dla angielskich słów i konstrukcji kodu (lepszy ratio tokenów/słowo dla angielskiego niż np. polskiego).
- **Budżet:** Ograniczenie wielkości słownika (np. 100k elementów) wymusza decyzje – co jest częstsze, to dostaje krótszy token.

**Tokeny specjalne (kontrola struktury):**
- `<unk>` – nieznany znak (słowo poza słownikiem, rzadkie w BPE).
- `<s>`, `</s>` – początek i koniec sekwencji (zdanie).
- `<system>`, `<user>`, `<assistant>` – znaczniki roli w konwersacji (dostrojone pod chat, jak na slajdzie).

**Padding i stała długość:**
- Transformer wymaga wejścia o **stałej długości** (batch processing).
- Krótsze sekwencje są uzupełniane tokenami `<pad>` (z prawej strony, jak na slajdzie).
- Dłuższe są przycinane (truncate) lub dzielone na chunki (jeśli przekraczają „context window").

---

### **4. Praktyczne Konsekwencje**

| Aspekt | Wpływ |
|--------|-------|
| **Długość kontekstu** | Model z oknem 128k tokenów nie oznacza 128k słów – „Szczęście" może być 2-3 tokenami. Rzeczywista liczba słów to ~60-70% liczby tokenów (zależy od języka). |
| **Koszt API** | Płaci się za tokeny (wejście + wyjście), nie za słowa. Kod z wieloma spacjami/znakami specjalnymi może być droższy. |
| **Języki „uboższe"** | Polski w tokenizerze treningowym na głównie angielskich danych będzie wymagał więcej tokenów na słowo (mniej efektywny). |
| **Reversibility** | Tokenizacja jest deterministyczna, ale nie zawsze czytelna dla człowieka – „ tokenizer" może podzielić słowo w środku morfemu. |

**Podsumowanie:** Tokenizer to „brama" między tekstem zrozumiałym dla człowieka a tensorami liczb zrozumiałymi dla Transformerów. BPE zapewnia balans między rozmiarem słownika a zdolnością do reprezentowania dowolnego tekstu (poprzez subwordy), przy czym tokenizer jest integralną częścią modelu (trening osobny, specyficzny dla języków i domen).


#WYKŁAD11 