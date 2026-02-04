**GAN (Generative Adversarial Networks)**
### 1. Idea – gra przeciwników
Zamiast uczyć jedną sieć do generowania, stawiamy dwóch graczy w **grze przeciwnej** (minimax):
- **Generator (G):** Tworzy fałszywe dane (losuje punkt z przestrzeni ukrytej → generuje obraz). Celem jest oszukanie dyskryminatora.
- **Dyskryminator (D):** Klasyfikuje „prawdziwe vs fałszywe”. Celem jest wykrycie podróbek.

**Intuicja:** G to fałszerz banknotów, D to policjant. Im lepszy D, tym lepszy musi być G – i odwrotnie. Rywalizacja wymusza jakość.

### 2. Uczenie – równoczesne, ale zamrożone
Trening odbywa się na przemian (lub w krokach):
1. **Uczymy D:** Pokazujemy realne próbki i generowane przez G. Dostosowuje wagi, by lepiej rozróżniać (kara za błędną klasyfikację).
2. **Uczymy G:** Zamrażamy wagi D (nie zmienia się), ale **propagujemy błąd wstecz przez cały układ G→D**. Kara dla G to moment, gdy D poprawnie wykrywa fałszywkę – generator uczy się „bardziej oszukiwać”.

**Pułapka:** Brak „ładnego” postępu jak w klasyfikacji – krzywe loss oscylują (instabilność treningu).

### 3. Różnica względem VAE [[Podział autokoderów]]

| Cecha | VAE | GAN |
|-------|-----|-----|
| **Struktura** | Enkoder + Dekoder | Tylko Generator (bez enkodera) + Dyskryminator |
| **Uczenie** | Porównanie z oryginałem (rekonstrukcja) | Rywalizacja (adwersarial) |
| **Jakość** | Rozmyte obrazy (ograniczenie funkcji straty) | Ostre, realistyczne (ale niestabilne) |
| **Kontrola** | Gładka przestrzeń ukryta (interpolacja) | Brak gwarancji struktury latent space |

**Kluczowe dla egzaminu:**  
GAN nie ma enkodera – nie potrafi „skompresować” istniejącego obrazu do wektora (brak inferencji). Potrafi tylko **generować** nowe próbki z losowego szumu. Do kompresji + generowania służy VAE.

#WYKŁAD13 