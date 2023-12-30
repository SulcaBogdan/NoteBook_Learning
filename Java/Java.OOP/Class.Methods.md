# Metodele claselor

Am vorbit in capitolul `Java.Methods` că metodele sunt declarate într-o clasă și că sunt folosite pentru a efectua anumite acțiuni:

```java
public class Main {
  static void myMethod() {
    System.out.println("Hello World!");
  }
}
```

`myMethod()` afișează un text (acțiunea) atunci când este apelată. Pentru a apela o metodă, scrie numele metodei urmat de două paranteze `()` și un punct și virgulă `;`

```java
public class Main {
  static void myMethod() {
    System.out.println("Hello World!");
  }

  public static void main(String[] args) {
    myMethod();
  }
}

output:
Hello World!
```

## `Static` vs `Public`


Adesea vei vedea programe Java care au atribute și metode fie statice, fie publice.

În exemplul de mai sus, am creat o metodă statică, ceea ce înseamnă că poate fi accesată fără a crea un obiect al clasei, spre deosebire de public, care poate fi accesat doar de obiecte:

Un exemplu pentru a evidenția diferențele dintre metodele `statice` și `publice`:


```java
public class Main {
  // Static method
  static void myStaticMethod() {
    System.out.println("Static methods can be called without creating objects");
  }

  // Public method
  public void myPublicMethod() {
    System.out.println("Public methods must be called by creating objects");
  }

  // Main method
  public static void main(String[] args) {
    myStaticMethod(); // Call the static method
    // myPublicMethod(); 

    Main myObj = new Main(); // Create an object of Main
    myObj.myPublicMethod(); // Call the public method on the object
  }
}

output:
Static methods can be called without creating objects
Public methods must be called by creating objects
```

## Accesarea metodelor cu un obiect

```java
// Create a Main class
public class Main {
 
  // Create a fullThrottle() method
  public void fullThrottle() {
    System.out.println("The car is going as fast as it can!");
  }

  // Create a speed() method and add a parameter
  public void speed(int maxSpeed) {
    System.out.println("Max speed is: " + maxSpeed);
  }

  // Inside main, call the methods on the myCar object
  public static void main(String[] args) {
    Main myCar = new Main();   // Create a myCar object
    myCar.fullThrottle();      // Call the fullThrottle() method
    myCar.speed(200);          // Call the speed() method
  }
}

The car is going as fast as it can!
Max speed is: 200
```

Exemplu explicat
1) Am creat o clasă `Main` personalizată cu cuvântul cheie `class`.

2) Am creat metodele `fullThrottle()` și `speed()` în clasa `Main`.

3) Metoda `fullThrottle()` și metoda `speed()` vor afișa un text atunci când sunt apelate.

4) Metoda `speed()` acceptă un parametru int numit `maxSpeed` - vom folosi acest lucru în pasul `8`.

5) Pentru a folosi clasa `Main` și metodele sale, trebuie să creăm un obiect al clasei `Main`.

6) Apoi, mergi la metoda `main()`, pe care deja o cunoști, fiind o metodă Java încorporată care rulează programul tău (oricodul din interiorul lui main este executat).

7) Folosind cuvântul cheie `new`, am creat un obiect cu numele `myCar`.

8) Apoi, apelăm metodele `fullThrottle()` și `speed()` pe obiectul `myCar` și rulăm programul folosind numele obiectului (`myCar`), urmat de un punct (`.`), urmat de numele metodei (`fullThrottle();` și `speed(200);`). Observă că adăugăm un parametru int de 200 în interiorul metodei.

### Ține minte că...
Punctul (`.`) este folosit pentru a accesa atributele și metodele obiectului.

Pentru a apela o metodă în Java, scrie numele metodei urmat de un set de paranteze `()`, urmat de un punct și virgulă (`;`).

O clasă trebuie să aibă un nume de fișier corespunzător (`Main` și `Main.java`).

## Folosirea a mai multor clase

Așa cum am specificat în capitolul Clase, este o practică bună să creezi un obiect al unei clase și să-l accesezi într-o altă clasă.

Ține minte că numele fișierului Java ar trebui să se potrivească cu numele clasei. În acest exemplu, am creat două fișiere în același director:

Main.java
Second.java


Main.java:
```java
public class Main {
  public void fullThrottle() {
    System.out.println("The car is going as fast as it can!");
  }

  public void speed(int maxSpeed) {
    System.out.println("Max speed is: " + maxSpeed);
  }
}
```

Second.java:

```java
class Second {
  public static void main(String[] args) {
    Main myCar = new Main();     // Create a myCar object
    myCar.fullThrottle();      // Call the fullThrottle() method
    myCar.speed(200);          // Call the speed() method
  }
}
```

Output:

```
The car is going as fast as it can!
Max speed is: 200
```

