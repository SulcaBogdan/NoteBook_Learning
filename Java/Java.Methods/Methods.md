# Metodele in Java


O metodă este un bloc de cod care se execută doar atunci când este apelat.

Puteți furniza date, cunoscute sub numele de parametri, unei metode.

Metodele sunt utilizate pentru a efectua anumite acțiuni și sunt cunoscute și sub numele de funcții.

De ce să folosim metodele? Pentru a reutiliza codul: definiți codul o dată și utilizați-l de mai multe ori.

## Crearea unei Metode

O metodă trebuie declarată în cadrul unei clase. Este definită cu numele metodei, urmat de paranteze (). Java furnizează unele metode predefinite, cum ar fi System.out.println(), dar puteți crea și propriile metode pentru a efectua anumite acțiuni:

```java
public class Main {
  static void myMethod() {
    // blocul de cod
  }
}
```

**Explicație Exemplu**

`myMethod()` este numele metodei.

`static` înseamnă că metoda aparține clasei Main și nu unui obiect al clasei Main. Vei învăța mai multe despre obiecte și cum să accesezi metodele prin obiecte mai târziu în acest tutorial.

`void` înseamnă că această metodă nu are o valoare de returnare. Vei învăța mai multe despre valorile de returnare mai târziu în acest capitol.

## Apelarea unei Metode

Pentru a apela o metodă în Java, scrie numele metodei urmat de două paranteze `()` și un punct și virgulă `;`

În exemplul următor, `myMethod()` este folosită pentru a afișa un text (acțiunea) atunci când este apelată:

```java
public class Main {
  static void myMethod() {
    System.out.println("I just got executed!");
  }

  public static void main(String[] args) {
    myMethod();
  }
}

output:
I just got executed!
```

O metodă poate fi, de asemenea, apelată de mai multe ori:

```java
public class Main {
  static void myMethod() {
    System.out.println("I just got executed!");
  }

  public static void main(String[] args) {
    myMethod();
    myMethod();
    myMethod();
  }
}

output:
I just got executed!
I just got executed!
I just got executed!
```






