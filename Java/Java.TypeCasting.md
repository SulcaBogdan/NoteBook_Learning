# Type casting in Java

## Conversia Tipurilor în Java

Conversia tipurilor se referă la atunci când atribui o valoare a unui tip primitiv la alt tip.

În Java, există două tipuri de conversie:

### Conversie Largă (automată) - convertirea unui tip mai mic într-un tip mai mare
`byte` `->` `short` `->` `char` `->` `int` `->` `long` `->` `float` `->` `double`

### Conversie Îngustă (manuală) - convertirea unui tip mai mare într-un tip mai mic
`double` `->` `float` `->` `long` `->` `int` `->` `char` `->` `short` `->` `byte`

### Conversie Largă

Conversia largă se face automat atunci când se trece de la un tip de dimensiune mai mică la unul de dimensiune mai mare:


```java
public class Main {
  public static void main(String[] args) {
    int myInt = 9;
    double myDouble = myInt; 

    System.out.println(myInt);      
    System.out.println(myDouble);   
  }
}

output:
9
9.0
```

### Conversie Îngustă

Conversia îngustă trebuie făcută manual, plasând tipul între paranteze în fața valorii:

```java
public class Main {
  public static void main(String[] args) {
    double myDouble = 9.78d;
    int myInt = (int) myDouble; // Manual casting: double to int

    System.out.println(myDouble);   // Outputs 9.78
    System.out.println(myInt);      // Outputs 9
  }
}

output:
9.78
9
```




