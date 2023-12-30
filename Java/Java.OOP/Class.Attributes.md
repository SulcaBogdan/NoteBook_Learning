# Atributele Clasei

În capitolul anterior, am folosit termenul "`variabilă`" pentru x în exemplu (așa cum este arătat mai jos). De fapt, este un `atribut` al clasei. Sau ai putea spune că atributele clasei sunt variabile într-o clasă:

```java
public class Main {
  int x = 5;
  int y = 3;
}
```
Am creat clasa `Main` cu 2 `atribute` `x` si `y`.

Un alt termen pentru atributele clasei este `câmpuri` (`fields`).

## Accesarea Atributelor

Poți accesa atributele prin crearea unui obiect al clasei și folosind sintaxa punct (`.`):

Următorul exemplu va crea un obiect al clasei `Main`, cu numele `myObj`. Folosim atributul `x` al obiectului pentru a afișa valoarea sa:

```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main myObj = new Main();
    System.out.println(myObj.x);
  }
}

output:
5
```

## Modificarea Atributelor

```java
public class Main {
  int x;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 40;
    System.out.println(myObj.x);
  }
}

output:
40
```

Sau să suprascrii valorile existente:

```java
public class Main {
  int x = 10;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 25; // x is now 25
    System.out.println(myObj.x);
  }
}

output:
25
```

Dacă nu dorești posibilitatea de a suprascrie valorile existente, declară atributul ca `final`:

```java
public class Main {
  final int x = 10;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 25; // will generate an error: cannot assign a value to a final variable
    System.out.println(myObj.x);
  }
}

output:
Main.java:6: error: cannot assign a value to final variable x
    myObj.x = 25;
         ^
1 error
```

Cuvântul cheie `final` este util atunci când dorești ca o variabilă să stocheze întotdeauna aceeași valoare, cum ar fi `PI` (3,14159...).

Cuvântul cheie `final` este numit "`modifier`". Vei învăța mai multe despre acestea în Capitolul Modificatori Java.

## Obiecte multiple


Dacă creezi mai multe obiecte ale unei clase, poți schimba valorile atributelor într-un obiect, fără a afecta valorile atributelor în celelalte:

```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main myObj1 = new Main();  // Object 1
    Main myObj2 = new Main();  // Object 2
    myObj2.x = 25;
    System.out.println(myObj1.x);  // Outputs 5
    System.out.println(myObj2.x);  // Outputs 25
  }
}

output:
5
25
```

## Atribute multiple

Putem specifica cate atribute dorim

```java
public class Main {
  String fname = "John";
  String lname = "Doe";
  int age = 24;

  public static void main(String[] args) {
    Main myObj = new Main();
    System.out.println("Name: " + myObj.fname + " " + myObj.lname);
    System.out.println("Age: " + myObj.age);
  }
}

output:
Name: John Doe
Age: 24
```






