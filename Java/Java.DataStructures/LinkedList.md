# LinkedList in Java

În capitolul anterior, ai învățat despre clasa `ArrayList`. Clasa `LinkedList` este aproape identică cu `ArrayList`:

```java
// Import the LinkedList class
import java.util.LinkedList;

public class Main {
  public static void main(String[] args) {
    LinkedList<String> cars = new LinkedList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    System.out.println(cars);
  }
}
```

## ArrayList vs. LinkedList
Clasa `LinkedList` este o colecție care poate conține multe obiecte de același tip, la fel ca `ArrayList`.

Clasa `LinkedList` are toate metodele aceleași ca și clasa `ArrayList`, deoarece ambele implementează interfața `List`. Acest lucru înseamnă că poți adăuga elemente, schimba elemente, elimina elemente și șterge lista în același mod.

Cu toate acestea, în timp ce clasa `ArrayList` și clasa `LinkedList` pot fi utilizate în același mod, sunt construite foarte diferit.

### Cum funcționează `ArrayList`

Clasa `ArrayList` are un array regulat în interior. Când este adăugat un element, este plasat în array. Dacă array-ul nu este suficient de mare, este creat un array nou, mai mare, pentru a înlocui cel vechi, iar cel vechi este eliminat.

### Cum funcționează `LinkedList`

`LinkedList` stochează elementele sale în "containere". Lista are un `link` către primul container, iar fiecare container are un `link` către următorul container din listă. Pentru a adăuga un element în listă, elementul este plasat într-un container nou și acel container este legat de unul dintre celelalte containere din listă.


### Folosește `ArrayList` pentru stocarea și accesarea datelor, iar `LinkedList` pentru manipularea datelor.


## Metodele LinkedList

În multe cazuri, `ArrayList` este mai eficient deoarece este obișnuit să ai nevoie de acces la elemente aleatoare din listă, dar `LinkedList` furnizează mai multe metode pentru a efectua anumite operații mai eficient:


| Metodă        | Descriere                                      |
| ------------- | ---------------------------------------------- |
| `addFirst()`  | Adaugă un element la începutul listei.          |
| `addLast()`   | Adaugă un element la sfârșitul listei.          |
| `removeFirst()`| Elimină un element de la începutul listei.      |
| `removeLast()` | Elimină un element de la sfârșitul listei.      |
| `getFirst()`   | Obține elementul de la începutul listei.        |
| `getLast()`    | Obține elementul de la sfârșitul listei.        |


