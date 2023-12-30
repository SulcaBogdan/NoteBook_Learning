# ArrayList in Java

Clasa `ArrayList` este un array redimensionabil, care se găsește în pachetul `java.util`.

Diferența dintre un `array încorporat` și un `ArrayList` în Java este că dimensiunea unui array nu poate fi modificată (dacă vrei să adaugi sau să elimini elemente dintr-un array, trebuie să creezi unul nou). În timp ce elemente pot fi adăugate și eliminate dintr-un `ArrayList` oricând dorești. Sintaxa este, de asemenea, ușor diferită:

```java
import java.util.ArrayList; // import the ArrayList class

ArrayList<String> cars = new ArrayList<String>(); // Create an ArrayList object
```

## Adaugarea elementelor

Clasa ArrayList are multe metode utile. De exemplu, pentru a adăuga elemente la ArrayList, folosește metoda `add()`:


```java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    System.out.println(cars);
  }
}

output:
[Volvo, BMW, Ford, Mazda]
```

## Accesarea unui element

Pentru a accesa un element în ArrayList, folosește metoda `get()` și referă-te la numărul de index:

```java
cars.get(0);

output:
Volvo
```

## Modificarea unui element

Pentru a modifica un element, folosește metoda `set()` și referă-te la numărul de index:


```java
cars.set(0, "Opel");

list is now [Opel, BMW, Ford, Mazda]
```

## Stergerea unui element
Pentru a elimina un element, folosește metoda `remove()` și referă-te la numărul de index:


```java
cars.remove(0);

list is now [BMW, Ford, Mazda]
```
Pentru a elimina toate elementele din ArrayList, folosește metoda `clear()`:

```java
cars.clear();

list is now []
```

## Lungimea listei

Pentru a afla câte elemente are un ArrayList, folosește metoda `size`:

```java
cars.size();

returns 3
```

## Parcurgerea unui ArrayList

Parcurge elementele unui `ArrayList` cu un buclu `for`, și folosește metoda `size()` pentru a specifica de câte ori ar trebui să ruleze bucla:


```java
public class Main {
  public static void main(String[] args) {
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    for (int i = 0; i < cars.size(); i++) {
      System.out.println(cars.get(i));
    }
  }
}

output:
Volvo
BMW
Ford
Mazda
```
Poți, de asemenea, să parcurgi un ArrayList cu bucla `for-each`:


```java
public class Main {
  public static void main(String[] args) {
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    for (String i : cars) {
      System.out.println(i);
    }
  }

output:
Volvo
BMW
Ford
Mazda
```

## Alte tipuri


Elementele dintr-un `ArrayList` sunt, de fapt, `obiecte`. În exemplele de mai sus, am creat elemente (obiecte) de tip "String". Amintește-ți că un String în Java este un obiect (nu un tip primitiv).

 Pentru a utiliza alte tipuri, cum ar fi `int`, trebuie să specifici o clasă de împachetare echivalentă: `Integer`. Pentru alte tipuri primitive, folosește: `Boolean` pentru `boolean`, `Character` pentru `char`, `Double` pentru `double`, etc:


```java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> myNumbers = new ArrayList<Integer>();
    myNumbers.add(10);
    myNumbers.add(15);
    myNumbers.add(20);
    myNumbers.add(25);
    for (int i : myNumbers) {
      System.out.println(i);
    }
  }
}

output:
10
15
20
25
```


## Sortarea unui ArrayList

O altă clasă utilă din pachetul java.util este clasa `Collections`, care include metoda `sort()` pentru a sorta liste alfabetic sau numeric:

```java
import java.util.ArrayList;
import java.util.Collections;  // Import the Collections class

public class Main {
  public static void main(String[] args) {
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    Collections.sort(cars);  // Sort cars
    for (String i : cars) {
      System.out.println(i);
    }
  }
}

output:
BMW
Ford
Mazda
Volvo
```
Un alt exemplu:

```java
import java.util.ArrayList;
import java.util.Collections;  // Import the Collections class

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> myNumbers = new ArrayList<Integer>();
    myNumbers.add(33);
    myNumbers.add(15);
    myNumbers.add(20);
    myNumbers.add(34);
    myNumbers.add(8);
    myNumbers.add(12);

    Collections.sort(myNumbers);  // Sort myNumbers

    for (int i : myNumbers) {
      System.out.println(i);
    }
  }
}

output:
8
12
15
20
33
34
```


