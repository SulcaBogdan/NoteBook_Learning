# Scope in Java

În Java, variabilele sunt accesibile numai în regiunea în care sunt create. Aceasta se numește `Scope`.

## Method Scope

Variabilele declarate direct în interiorul unei metode sunt disponibile oriunde în metoda după linia de cod în care au fost declarate:

```java
public class Main {
  public static void main(String[] args) {

    // Code here CANNOT use x

    int x = 100;

    // Code here can use x
    System.out.println(x);
  }
}

output:
100
```

## Block Scope

Un bloc de cod se referă la tot codul dintre acolade `{}`.

Variabilele declarate în interiorul blocurilor de cod sunt accesibile numai prin codul dintre acolade, care urmează linia în care a fost declarată variabila:

```java
public class Main {
  public static void main(String[] args) {

    // Code here CANNOT use x

    { // This is a block

      // Code here CANNOT use x

      int x = 100;

      // Code here CAN use x
      System.out.println(x);

    } // The block ends here

  // Code here CANNOT use x

  }
}

output:
100
```






