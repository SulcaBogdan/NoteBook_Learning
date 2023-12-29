# Parametrii metodei

**Parametri și Argumente**

Informații pot fi transmise metodelor ca parametri. Parametrii acționează ca variabile în interiorul metodei.

Parametrii sunt specificați după numele metodei, în interiorul parantezelor. Puteți adăuga atât de mulți parametri cât doriți, pur și simplu îi separați cu o virgulă.

Exemplul următor are o metodă care primește un șir de caractere numit `fname` ca parametru. Când metoda este apelată, transmitem un prenume, care este utilizat în interiorul metodei pentru a afișa numele complet:

```java
public class Main {
  static void myMethod(String fname) {
    System.out.println(fname + " Refsnes");
  }

  public static void main(String[] args) {
    myMethod("Liam");
    myMethod("Jenny");
    myMethod("Anja");
  }
}

output:
Liam Refsnes
Jenny Refsnes
Anja Refsnes
```

## Parametrii multiplii

Putem avea cati parametrii dorim

```java
public class Main {
  static void myMethod(String fname, int age) {
    System.out.println(fname + " is " + age);
  }

  public static void main(String[] args) {
    myMethod("Liam", 5);
    myMethod("Jenny", 8);
    myMethod("Anja", 31);
  }
}

output:
Liam is 5
Jenny is 8
Anja is 31
```


Rețineți că atunci când lucrați cu mai mulți parametri, apelul metodei trebuie să aibă același număr de argumente ca și numărul de parametri, iar argumentele trebuie să fie transmise în aceeași ordine.


## `Return`

Cuvântul cheie `void`, folosit în exemplele de mai sus, indică faptul că metoda nu ar trebui să **returneze** o valoare. Dacă doriți ca metoda să returneze o valoare, puteți folosi un tip de date primitiv (cum ar fi `int`, `char`, etc.) în loc de `void` și utilizați cuvântul cheie `return` în interiorul metodei:

```java
public class Main {
  static int myMethod(int x) {
    return 5 + x;
  }

  public static void main(String[] args) {
    System.out.println(myMethod(3));
  }
}
output:
8
```

Acest exemplu returnează suma a două parametri ai unei metode:

```java
public class Main {
  static int myMethod(int x, int y) {
    return x + y;
  }

  public static void main(String[] args) {
    System.out.println(myMethod(5, 3));
  }
}

output:
8
```

Poți, de asemenea, să stochezi rezultatul într-o variabilă (recomandat, deoarece este mai ușor de citit și întreținut):


```java
public class Main {
  static int myMethod(int x, int y) {
    return x + y;
  }

  public static void main(String[] args) {
    int z = myMethod(5, 3);
    System.out.println(z);
  }
}

output:
8
```

## Metoda cu if..else

Este obișnuit să folosești instrucțiuni if...else în interiorul metodelor:

```java
public class Main {

  
  static void checkAge(int age) {

    if (age < 18) {
      System.out.println("Access denied - You are not old enough!");
    
    } else {
      System.out.println("Access granted - You are old enough!");
    }

  }

  public static void main(String[] args) {
    checkAge(20); 
  }
}

output:
Access granted - You are old enough!
```




