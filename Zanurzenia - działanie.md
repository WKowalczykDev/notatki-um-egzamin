### **1. Architektura Prostego Modelu (Skip-gram)**
Na podstawie schematu z obrazka — to **płytka sieć neuronowa** (MLP) z jedną warstwą ukrytą:

- **Wejście:** Słowo centralne w postaci **one-hot** (wektor o długości 10 000 — rozmiar słownika, jedna jedynka na pozycji słowa, reszta zer).
- **Warstwa Ukryta:** 300 neuronów (to jest kluczowe — **embedding**). Mnożenie macierzy 10 000 × 300 „kompresuje” słowo do wektora 300 liczb.
- **Wyjście:** **Softmax** nad całym słownikiem (10 000 klas) — przewidujemy prawdopodobieństwo wszystkich słów, które mogą wystąpić w kontekście danego słowa.

**Zamiast przewidywać słowo na podstawie kontekstu (CBOW), Skip-gram robi na odwrót:** z jednego słowa (input) przewiduje wiele słów z jego otoczenia (output — multilabel, bo w oknie może być kilka słów).

### **2. Okno Przesuwne (Generowanie Przykładów Treningowych)**
Skip-gram działa na zasadzie **przesuwnego okna** nad tekstem:

**Przykład (okno = 1):**
Zdanie: *„kot je mysz"*
- Input: **„je"** (one-hot) → Target: „kot" i „mysz" (dwa słowa kontekstowe do przewidzenia)
- Input: **„kot"** → Target: „je"
- Input: **„mysz"** → Target: „je"

Sieć jest uczona na milionach takich par (słowo, słowo_kontekstowe), „uświadamiając sobie", które słowa występują blisko siebie.

### **3. Podobieństwo Cosinusowe i „Luka Semantyczna"**
**Jak mierzymy podobieństwo?**
Na obrazku widzisz mnożenie wektora „ants" (300 cech) przez wektor wag dla „car". To jest **iloczyn skalarny**, który jest miarą podobieństwa cosinusowego (im mniejszy kąt między wektorami, tym wyższa wartość).

**Luka semantyczna (Latent Space):**
- **Wektory „tworzą się same":** Na początku są losowe. Podczas treningu (gradient descent) optymalizator przesuwa je w przestrzeni 300-wymiarowej tak, aby blisko siebie były słowa z podobnych kontekstów.
- **Niezrozumiałość dla człowieka:** Nie ma sensu pytać „co oznacza wymiar 47 wektora?". Wymiary nie mają nazw (nie są „futrzatość", „rozmiar"). To **czarna skrzynia** — matematycznie działa (podobieństwo cosinusowe), ale człowiek nie potrafi zinterpretować pojedynczej liczby.
- **Relacje algebraiczne:** Mimo „luki", przestrzech zachowuje logikę:  
  `wektor(król) - wektor(mężczyzna) + wektor(kobieta) ≈ wektor(królowa)`

### **4. Negative Sampling — Uczenie się przez Kontrast (Brak Zależności)**
W klasycznym modelu z softmaks musisz aktualizować wagi dla wszystkich 10 000 słów przy każdym przykładzie — to zbyt wolne.

**Rozwiązanie:** Zamieniamy problem na **klasyfikację binarną** (czy ta para słów ma sens, czy nie?):

- **Pozytywny przykład (Co JEST w relacji):** Prawdziwe słowo z kontekstu, np. („kot", „je") → etykieta **1**. Model uczy się, że te słowa do siebie pasują.

- **Negatywne przykłady (Czego NIE MA w relacji):** Losowo wybrane słowa, które **nie występują** w oknie kontekstowym, np. („kot", „samochód"), („kot", „trawa"), („kot", „biurko") → etykieta **0**.

**Intuicja "ludzka" — Uczenie się przez przeciwieństwo:**
Model nie uczy się tylko przez pokazywanie „kot + futro = tak". Uczy się również przez pokazywanie „kot + samolot = nie". To jest jak nauka pojęcia „przyjaciel" — nie wystarczy wiedzieć, że przyjaciel jest miły, trzeba też wiedzieć, że **wróg nie jest przyjacielem**.

Dzięki milionom takich negatywnych przykładów, model **definiuje granice pojęcia**: przyciąga wektor „kota" do „psa" (bo często pozytywne), ale **aktywnie odsuwa** go od „samochodu" czy „biurka" (bo widział je jako negatywne pary). Tworzy się wyraźny klaster „zwierzęta" oddzielony od „meble" czy „pojazdy".

### **5. Subsampling Częstych Słów (Usunięcie „the")**
Osobny problem: Słowa jak „the", „a", „is" pojawiają się w korpusie miliony razy, ale niosą **mało semantycznej informacji** (funkcja gramatyczna). Dominują w treningu, ale nie uczą modelu niczego ciekawego.

**Rozwiązanie:** Usunięcie (subsampling) — każde wystąpienie bardzo częstego słowa jest usuwane z treningu z pewnym prawdopodobieństwem (np. 80% dla „the"). Pozostawia się rzadsze, bardziej informatywne słowa (kot, je, mysz), co przyspiesza uczenie i poprawia jakość zanurzeń.

#WYKŁAD10 