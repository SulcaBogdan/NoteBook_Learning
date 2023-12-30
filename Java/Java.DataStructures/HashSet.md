# HashSet in Java

Un HashSet este o colecție de elemente în care fiecare element este unic, și este găsit în pachetul `java.util`:


```java
import java.util.HashSet; // Import the HashSet class

HashSet<String> cars = new HashSet<String>();
```

## Adaugarea de elemente intr-un HashSet

Clasa `HashSet` are multe metode utile. De exemplu, pentru a adăuga elemente în ea, folosește metoda `add()`:


```java
// Import the HashSet class
import java.util.HashSet;

public class Main {
  public static void main(String[] args) {
    HashSet<String> cars = new HashSet<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("BMW");
    cars.add("Mazda");
    System.out.println(cars);
  }
}

output:
[Volvo, Mazda, Ford, BMW]
```

Notă: În exemplul de mai sus, chiar dacă BMW este adăugat de două ori, apare doar o dată în set pentru că fiecare element într-un set trebuie să fie unic.


## Verifica daca exista un element

Pentru a verifica dacă un element există într-un `HashSet`, folosește metoda `contains()`:


```java
cars.contains("Mazda");

output:
true
```

## Sterge un element din HashSet

Pentru a elimina un element, folosește metoda `remove()`:

```java
cars.remove("Volvo");

output:
[Mazda, Ford, BMW]
```

Pentru a elimina toate elementele, folosește metoda `clear()`:

```java
cars.clear();

output:
[]
```

## Dimensiunea unui HashSet


Pentru a afla câte elemente există, folosește metoda `size()`:

```java
cars.size()

output:
4
```

## Parcurgerea unui HashSet

Parcurge elementele unui `HashSet` cu un ciclu `for-each`:

```java
for (String i : cars) {
  System.out.println(i);
}

output:
Volvo
Mazda
Ford
BMW
```

## Alte tipuri

Elementele dintr-un `HashSet` sunt, de fapt, obiecte. În exemplele de mai sus, am creat elemente (obiecte) de tip "String". Amintește-ți că un String în Java este un obiect (nu un tip primitiv). Pentru a folosi alte tipuri, cum ar fi int, trebuie să specifici o clasă înveliș echivalentă: Integer. Pentru alte tipuri primitive, folosește: Boolean pentru boolean, Character pentru char, Double pentru double, etc:

```java
import java.util.HashSet;

public class Main {
  public static void main(String[] args) {

    // Create a HashSet object called numbers
    HashSet<Integer> numbers = new HashSet<Integer>();

    // Add values to the set
    numbers.add(4);
    numbers.add(7);
    numbers.add(8);

    // Show which numbers between 1 and 10 are in the set
    for(int i = 1; i <= 10; i++) {
      if(numbers.contains(i)) {
        System.out.println(i + " was found in the set.");
      } else {
        System.out.println(i + " was not found in the set.");
      }
    }
  }
}

output:
1 was not found in the set.
2 was not found in the set.
3 was not found in the set.
4 was found in the set.
5 was not found in the set.
6 was not found in the set.
7 was found in the set.
8 was found in the set.
9 was not found in the set.
10 was not found in the set.
```