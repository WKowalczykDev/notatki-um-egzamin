[[MLP]]

### 1. Logity (_logits_)

**Co to:** Surowe wyjście z **ostatniej warstwy liniowej**, przed nałożeniem funkcji softmax (lub sigmoid).

**Intuicja:** To „nieznormalizowane” prawdopodobieństwa – dowolne liczby rzeczywiste (nie muszą sumować się do 1). Im wyższy logit dla danej klasy, tym model jest bardziej przekonany.

**Po co to rozróżniać?**

- Softmax robi z logitów rozkład prawdopodobieństwa: σ(zi​)=∑ezj​ezi​​
- W uczeniu (cross-entropy) liczymy stratę właśnie na logitach – mają lepsze właściwości gradientowe niż wartości po softmaxie (unikamy „zanikających” gradientów).    

**Pułapka:** Mówimy „model wypluł logity 2.5, -1.0, 0.3” – to oznacza, że przed softmaxem klasa 1 miała najwyższą „siłę głosu”.


### 2. Twierdzenie Cybenki (Universal Approximation Theorem)

**Co to:** Twierdzenie mówiące, że **pojedyncza warstwa ukryta** w MLP (z odpowiednią liczbą neuronów i nieliniową funkcją aktywacji, np. sigmoid lub ReLU) może **dowolnie dokładnie aproksymować każdą funkcję ciągłą** na danym obszarze.

**Intuicja:** Niezależnie od tego, jak skomplikowana jest zależność między wejściem a wyjściem (np. funkcja decyzyjna w klasyfikacji), istnieje MLP, który ją „nauczy” – pod warunkiem, że ma wystarczająco dużo neuronów w warstwie ukrytej.

**Dlaczego to ważne na egzaminie:**
- **Gwarancja możliwości:** To dlaczego możemy używać MLP do dowolnej regresji i klasyfikacji (w tym regresji na logitach). Sieć ma **uniwersalną moc aproksymacyjną**.
- **Ale uwaga:** Twierdzenie mówi, że taka sieć **istnieje**, ale nie mówi, jak ją znaleźć (nie gwarantuje, że nasz algorytm uczenia do niej dojdzie) ani ile neuronów potrzeba (może być ich astronomicznie dużo).

**Podsumowanie:** MLP z nieliniowością to „uniwersalny aproksymator” – teoretycznie potrafi nauczyć się każdego zagadnienia, dlatego jest podstawowym narzędziem w uczeniu maszynowym.


#WYKŁAD13 
