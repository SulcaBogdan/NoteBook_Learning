# Iterator in Java

Un Iterator este un obiect care poate fi folosit pentru a parcurge colecții, cum ar fi ArrayList și HashSet. Este numit "iterator" deoarece "iterarea" este termenul tehnic pentru parcurgere.

Pentru a folosi un `Iterator`, trebuie să îl importați din pachetul `java.util`.

Metoda `iterator()` poate fi folosită pentru a obține un Iterator pentru orice colecție:


```java
// Import the ArrayList class and the Iterator class
import java.util.ArrayList;
import java.util.Iterator;

public class Main {
  public static void main(String[] args) {

    // Make a collection
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");

    // Get the iterator
    Iterator<String> it = cars.iterator();

    // Print the first item
    System.out.println(it.next());
  }
}

output:
Volvo
```

Pentru a parcurge o colecție, folosește metodele `hasNext()` și `next()` ale Iteratorului:


```java
while(it.hasNext()) {
  System.out.println(it.next());
}

output:
Volvo
BMW
Ford
Mazda
```


Iteratorii sunt proiectați să schimbe ușor colecțiile prin care parcurg. Metoda `remove()` poate elimina elemente dintr-o colecție în timpul parcurgerii.

```java
import java.util.ArrayList;
import java.util.Iterator;

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(12);
    numbers.add(8);
    numbers.add(2);
    numbers.add(23);
    Iterator<Integer> it = numbers.iterator();
    while(it.hasNext()) {
      Integer i = it.next();
      if(i < 10) {
        it.remove();
      }
    }
    System.out.println(numbers);
  }
}

output:
[12, 23]
```