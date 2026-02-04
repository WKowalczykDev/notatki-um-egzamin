## Idea ogólna: "Normalne" vs "Dziwne"

Algorytm zakłada, że **większość danych jest "normalna"** i tworzy pewien przewidywalny wzorzec. Anomalie to punkty, które **nie pasują** do tego wzorca — są "mało prawdopodobne".


Dla każdej cechy liczymy średnią i wariancję - jak bardzo wartości się rozpraszają

Łączymy prawdopodobieństwa:
Liczymy prawdopodobieństwo całkowite (np. iloczyn prawdopodobieństw)

Detekcja anomalii to oznacza, że nasze prawdopodobieństwo całkowite jest mniejsze niż **ε**
Wybieramy próg ε. Jeśli p(x)<ε → **ANOMALIA**.


### **Jak dobrać ε?**

| Sposób       | Kiedy stosować          | Przykład                                                                                                              |
| ------------ | ----------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Z góry**   | Znasz dziedzinę         | "Wiem, że ok. 1% maszyn się psuje" → ε takie, że 1% danych będzie poniżej                                             |
| **Z danych** | Masz oznaczone anomalie | Uczysz na danych "normalnych", testujesz różne ε na danych z anomaliami, wybierasz najlepsze (np. najwyższy F1-score) |

### Patrzymy na współkorelacje różnych danych
Bardzo kosztowne,
Dane muszą być "znośnie" gaussowskie
Jeśli cecha ma **rozkład wykładniczy** (np. czas oczekiwania — zawsze dodatni, długi ogon):
**Rozwiązanie**: Transformacja np. log(x) przed zastosowaniem algorytmu.


w Python:
`from sklearn.covariance import EllipticEnvelope`

#WYKŁAD6 