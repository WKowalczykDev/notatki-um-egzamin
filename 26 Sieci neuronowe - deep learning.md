Często dane nie są tak proste do zaklasyfikowania:
Nie jest to problem prostej regresji liniowej zeby określić do jakiego klastra mamy je dostosować.

W deep learningu warstwy tworzą coraz wyższy poziom abstrakcji jeżeli chodzi o klasyfikacje cech

Bardzo trudno rozróżnić komputerowi zdjecia - bo to tak naprawde gigamacierz.
Dlatego robimy **sieć neuronową** mającą na celu jak najbardziej uprościć niektóre zależności dla komputera:

### Przykładowy przebieg
Dane wejściowe (piksele, surowe cechy)
    ↓ [Warstwa 1] — wykrywa proste wzorce (krawędzie, linie)
    ↓ [Warstwa 2] — łączy je w kształty (okręgi, tekstury)
    ↓ [Warstwa 3] — rozpoznaje części obiektów (ucho, oko)
    ↓ [Warstwa N] — klasyfikuje cały obiekt (to jest kot)

### Działanie deep-learning
1. **Automatyczna ekstrakcja cech** — nie musisz ręcznie wymyślać, jak opisać dane
2. **Nieliniowe mapowanie** — sieć "wygina" przestrzeń, by nieliniowo separowalne klastry stały się liniowo separowalne w wyższych warstwach
3. **Głęboka hierarchia** — złożone koncepty budowane z prostych składowych

#WYKŁAD7
