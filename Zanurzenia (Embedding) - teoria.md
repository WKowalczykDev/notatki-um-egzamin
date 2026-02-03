### **Różnica: One-hot Encoding vs Embedding**

**One-hot encoding (stare podejście):**
- „Kot” = `[1, 0, 0, 0, ...]` (10000 zer, jedna jedynka na pozycji słowa „kot”)
- „Pies” = `[0, 1, 0, 0, ...]`
- **Problem:** Każde słowo to osobny wymiar. Nie ma relacji między „kotem” a „psem” (odległość euklidesowa między wektorami jest taka sama jak między „kotem” a „samochodem”).

**Zanurzenie (embedding):**
- „Kot” = `[0.2, -0.5, 0.8, ...]` (np. 100 lub 300 wymiarów)
- „Pies” = `[0.3, -0.4, 0.7, ...]`
- **Klucz:** Słowa o podobnym znaczeniu mają **podobne wektory** (bliskie w przestrzeni euklidesowej).

---

### **Skąd się biorą te liczby? (Uczenie nienadzorowane)**

Zanurzeń się **nie wymyśla ręcznie** – są uczona na ogromnych korpusach tekstu (np. Wikipedia, książki) w sposób **nienadzorowany** (bez etykiet):

**Idea:** „Słowo jest znane przez otoczenie, w jakim występuje” (Firth, 1957).
- Jeśli „kot” i „pies” często pojawiają się w podobnych kontekstach („... jeść”, „... śpi na kanapie”, „... ma cztery łapy”), to ich wektory powinny być zbliżone.
- Model (np. Word2Vec, GloVe, FastText) przesuwa wektory tak, aby podobne konteksty dawały zbliżone reprezentacje.

**Przykład słynny:**
```
Wektor("król") - Wektor("mężczyzna") + Wektor("kobieta") ≈ Wektor("królowa")
```
Sieć nauczyła się relacji „płci” i „monarchii” czysto z tekstu, bez etykietowania.

---

### **Jak to działa w sieciach neuronowych?**

1. **Warstwa Embedding** (w Keras: `Embedding(vocab_size, embedding_dim)`):
   - Mapuje indeks słowa (np. 247) na gęsty wektor (np. 100 liczb).
   - Te wektory są **inicjalizowane losowo**, ale **uczone się podczas treningu** (lub wczytywane z pre-trained jak Word2Vec).

2. **Dlaczego to działa?**
   - Zamiast 10 000 wymiarów (one-hot), masz 100 wymiarów (gęsty).
   - Sieć widzi, że „kot” i „tiger” mają bliskie wektory, więc cechy nauczone dla kota pomagają przy tygrysie (transfer wewnątrz języka).

---

### **Podsumowanie**

- **Embedding to nie tylko wektor** – to wektor **semantyczny**, gdzie odległość = podobieństwo znaczenia.
- **Uczone nienadzorowano** – wystarczy dużo tekstu, nie potrzeba ręcznego etykietowania.
- **Zastosowania:** NLP (input do RNN/Transformerów), wizualizacja (można rzutować na 2D i zobaczyć „chmury” synonimów), rekomendacje (embeddingi użytkowników i produktów).

[[]]

#WYKŁAD10 