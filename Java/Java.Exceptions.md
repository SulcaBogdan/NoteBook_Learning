# Exceptiile in Java

La executarea codului Java, pot apărea diferite erori: erori de cod realizate de programator, erori datorate unui input greșit sau alte situații neprevăzute.

Când apare o eroare, Java se va opri în mod normal și va genera un mesaj de eroare. Termenul tehnic pentru aceasta este: Java va arunca o excepție (va genera o eroare).

## try and catch
Declarația `try` vă permite să definiți un bloc de cod care să fie testat pentru erori în timpul execuției.

Declarația `catch` vă permite să definiți un bloc de cod care să fie executat, dacă apare o eroare în blocul `try`.

Cuvintele cheie `try` și `catch` vin în perechi:

```java
try {
  //  Block of code to try
}
catch(Exception e) {
  //  Block of code to handle errors
}
```
```java
public class Main {
  public static void main(String[ ] args) {
    int[] myNumbers = {1, 2, 3};
    System.out.println(myNumbers[10]); // error!
  }
}

output:
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 10
        at Main.main(Main.java:4)
```

Dacă apare o eroare, putem folosi `try`...catch pentru a prinde eroarea și a executa un cod pentru a o gestiona:


```java
public class Main {
  public static void main(String[ ] args) {
    try {
      int[] myNumbers = {1, 2, 3};
      System.out.println(myNumbers[10]);
    } catch (Exception e) {
      System.out.println("Something went wrong.");
    }
  }
}

output:
Something went wrong.
```

## `Finally`

`Finally` vă permite să executați cod, după try...catch, indiferent de rezultat:

```java
public class Main {
  public static void main(String[] args) {
    try {
      int[] myNumbers = {1, 2, 3};
      System.out.println(myNumbers[10]);
    } catch (Exception e) {
      System.out.println("Something went wrong.");
    } finally {
      System.out.println("The 'try catch' is finished.");
    }
  }
}

output:
Something went wrong.
The 'try catch' is finished.
```

## Cuvântul-cheie `throw`

Instrucția `throw` vă permite să creați o eroare personalizată.

Instrucția `throw` este folosită împreună cu un tip de excepție. Există multe tipuri de excepții disponibile în Java: `ArithmeticException`, `FileNotFoundException`, `ArrayIndexOutOfBoundsException`, `SecurityException`, etc:


```java
public class Main {
  static void checkAge(int age) {
    if (age < 18) {
      throw new ArithmeticException("Access denied - You must be at least 18 years old.");
    }
    else {
      System.out.println("Access granted - You are old enough!");
    }
  }

  public static void main(String[] args) {
    checkAge(15); // Set age to 15 (which is below 18...)
  }
}

output:
Exception in thread "main" java.lang.ArithmeticException: Access denied - You must be at least 18 years old.
        at Main.checkAge(Main.java:4)
        at Main.main(Main.java:12)
```

```java
checkAge(20);

output:
Access granted - You are old enough!
```

