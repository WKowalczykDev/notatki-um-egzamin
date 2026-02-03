### **1. Transfer Learning (Uczenie transferowe)**
Pobierasz model wytrenowany na ogromnym zbiorze (np. ImageNet) i używasz go jako **ekstraktora cech** dla własnego, mniejszego problemu.

**Implementacja:**
1.  **Baza:** Załaduj pre-trained model (np. ResNet), usuń jego ostatnie warstwy (klasyfikator) i dodaj nowe (dla Twoich klas).
2.  **Zamrożenie:** Ustaw `base_model.trainable = False` — blokujesz wagi już nauczonych warstw.
3.  **Trenowanie:** Uczysz **tylko** nowe warstwy na swoich danych. Zamrożone warstwy działają jak „czarna skrzynka” wykrywająca krawędzie/tekstury.

---

### **2. Fine-tuning (Dostrajanie)**
**Opcjonalny** krok po Transfer Learningu.

**Mechanizm:** Po wstępnym wytrenowaniu nowych warstw (krok 3 powyżej), **odmrażasz** część lub wszystkie zamrożone warstwy i trenujesz całość dalej, ale z **bardzo małym learning rate** (np. 10⁻⁵).

**Cel:** Delikatne dostrojenie ogólnych cech (np. „krawędź”) do specyfiki Twoich danych (np. „krawędź skrzydła pingwina”), bez zniszczenia ogólnej wiedzy modelu.

---

### **3. Kluczowa Różnica**

| Cecha | Transfer Learning (Feature Extraction) | Fine-tuning |
|-------|----------------------------------------|-------------|
| **Wagi pre-trained** | Zamrożone (`trainable=False`) | Odmrożone i aktualizowane |
| **Co się uczy?** | Tylko nowe warstwy | Cała sieć (lub jej głębsze partie) |
| **Learning rate** | Zwykły (np. 0.001) | Bardzo mały (np. 0.00001) |
| **Ryzyko** | Niskie (bezpieczne przy małych danych) | Wysokie (przeuczenie, jeśli danych za mało) |

---

### **4. Augmentacja (Data Augmentation) w TL**
Gdy masz **mało danych** (co jest normą w Transfer Learningu), augmentacja (obroty, odbicia, przycięcia) jest **kluczowa**:
- Zapobiega przeuczeniu się nowych warstw na małym zbiorze.
- Pozwala bezpiecznie „zamrozić” więcej warstw (mniej ryzyka).
- Jeśli masz bardzo mało danych → tylko Transfer Learning + augmentacja. Fine-tuning odpuszczasz lub robisz bardzo ostrożnie.

**Reguła:** Im mniej danych, tym więcej augmentacji i mniej fine-tuningu (lub wcale).

#WYKŁAD9 