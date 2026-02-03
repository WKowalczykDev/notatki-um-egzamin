Polega na konwersji danych wielowymiarowych do wektora jednowymiarowego
Jest to tzw. **zanurzenie obrazowe**

![[Pasted image 20260203081343.png]]

Spłaszczamy dane (operacja **Flatten**), aby połączyć dwie niekompatybilne części sieci CNN:
1. **Część splotowa (Conv + Pool)** — działa na obrazach (tensory 3D: wysokość × szerokość × kanały) i wykrywa cechy przestrzenne (gdzie coś jest). 
2. **Część klasyfikująca (Fully Connected / Dense / MLP)** — działa jak zwykła sieć neuronowa, która **wymaga wektora 1D** (lista liczb) na wejściu, aby podjąć decyzję „kot vs pies”.
#WYKŁAD8 