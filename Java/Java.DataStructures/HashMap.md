# HashMap in Java

În capitolul despre `ArrayList`, ai învățat că Arrays stochează elemente ca o colecție ordonată și trebuie să le accesezi cu un număr de index (de tip int). 

Un `HashMap`, în schimb, stochează elemente în perechi "`cheie/valoare`", și le poți accesa printr-un index de alt tip (de exemplu, un String).

Un obiect este folosit ca o cheie (index) către alt obiect (valoare). Poate să stocheze diferite tipuri: chei de tip String și valori de tip Integer, sau același tip, precum: chei de tip String și valori de tip String:

```java
import java.util.HashMap; // import the HashMap class

HashMap<String, String> capitalCities = new HashMap<String, String>();
```

## Adaugarea elementelor in HashMap

Clasa `HashMap` are multe metode utile. De exemplu, pentru a adăuga elemente în ea, folosește metoda `put()`:

```java
// Import the HashMap class
import java.util.HashMap;

public class Main {
  public static void main(String[] args) {
    // Create a HashMap object called capitalCities
    HashMap<String, String> capitalCities = new HashMap<String, String>();

    // Add keys and values (Country, City)
    capitalCities.put("England", "London");
    capitalCities.put("Germany", "Berlin");
    capitalCities.put("Norway", "Oslo");
    capitalCities.put("USA", "Washington DC");
    System.out.println(capitalCities);
  }
}

output:
{USA=Washington DC, Norway=Oslo, England=London, Germany=Berlin}
```

## Accesarea unui element din HashMap

Pentru a accesa o valoare în `HashMap`, folosește metoda `get()` și referă-te la cheie:


```java
capitalCities.get("England");

output:
London
```

## Stergerea unui element

Pentru a elimina un element, folosește metoda `remove()` și referă-te la cheie:

```java
capitalCities.remove("England");

HashMap-ul va arata asa {USA=Washington DC, Norway=Oslo, Germany=Berlin}
```
Pentru a elimina toate elementele, folosește metoda `clear()`:

```java
capitalCities.clear()

HashMap-ul va arata asa {}
```

## Dimensiunea unui HashMap

Pentru a afla câte elemente există, folosește metoda `size()`:

```java
capitalCities.size()
4
```

## Parcurgerea unui HashMap

Parcurge elementele unui `HashMap` cu un ciclu `for-each`.

Notă: Folosește metoda `keySet()` dacă vrei doar cheile și metoda `values()` dacă vrei doar valorile:

```java
// Print keys
for (String i : capitalCities.keySet()) {
  System.out.println(i);
}

output:
USA
Norway
England
Germany
```

```java
// Print values
for (String i : capitalCities.values()) {
  System.out.println(i);
}

output:
Washington DC
Oslo
London
Berlin
```

```java
// Print keys and values
for (String i : capitalCities.keySet()) {
  System.out.println("key: " + i + " value: " + capitalCities.get(i));
}

output:
key: USA value: Washington DC
key: Norway value: Oslo
key: England value: London
key: Germany value: Berlin
```


## Alte tipuri

Cheile și valorile dintr-un `HashMap` sunt, de fapt, obiecte. În exemplele de mai sus, am folosit obiecte de tip "String". Amintește-ți că un String în Java este un obiect (nu un tip primitiv). Pentru a folosi alte tipuri, cum ar fi int, trebuie să specifici o clasă înveliș echivalentă: `Integer`. Pentru alte tipuri primitive, folosește: `Boolean` pentru boolean, `Character` pentru char, `Double` pentru double, etc:

```java
// Import the HashMap class
import java.util.HashMap;

public class Main {
  public static void main(String[] args) {

    // Create a HashMap object called people
    HashMap<String, Integer> people = new HashMap<String, Integer>();


    // Add keys and values (Name, Age)
    people.put("John", 32);
    people.put("Steve", 30);
    people.put("Angie", 33);

    for (String i : people.keySet()) {
      System.out.println("key: " + i + " value: " + people.get(i));
    }
  }
}

output:
Name: Angie Age: 33
Name: Steve Age: 30
Name: John Age: 32
```



