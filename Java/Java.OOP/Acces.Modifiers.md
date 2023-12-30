# Java modificatorii de acces

Până acum, ești destul de familiarizat cu cuvântul cheie `public` care apare în aproape toate exemplele noastre:

```java
public class Main{
    // block of code
}
```

Cuvântul cheie `public` este un **modificator de acces**, ceea ce înseamnă că este folosit pentru a seta nivelul de acces pentru `clase`, `atribute`, `metode` și `constructori`.

### **Modificatorii sunt împărțiți în două grupuri:**

1. **Modificatori de Access** - controlează nivelul de acces
2. **Modificatori Non-Access** - nu controlează nivelul de acces, dar oferă alte funcționalități

### Pentru clase puteti folosii ori public or default

| Modifier | Descriere                                           |
|----------|-----------------------------------------------------|
| `public`   | Clasa este accesibilă de oricare altă clasă         |
| `default`  | Clasa este accesibilă doar de către clasele din același pachet. Acest lucru este folosit atunci când nu specifici un modificator. Vei învăța mai multe despre pachete în capitolul Pachete. |

### Pentru atribute, metode si constructori putem folosii urmatoarele:

| Modifier  | Descriere                                           |
|-----------|-----------------------------------------------------|
| `public`    | Codul este accesibil pentru toate clasele          |
| `private`   | Codul este accesibil doar în cadrul clasei declarate|
| `default`   | Codul este accesibil doar în același pachet. Acest lucru este folosit atunci când nu specifici un modificator. Vei învăța mai multe despre pachete în capitolul Pachete |
| `protected` | Codul este accesibil în același pachet și subclase. Vei învăța mai multe despre subclase și superclase în capitolul Moștenire |

## Modificatorii Non-Access

### Pentru clase, poți folosi fie `final`, fie `abstract`:

| Modifier | Descriere                                           |
|----------|-----------------------------------------------------|
| `final`    | Clasa nu poate fi moștenită de alte clase (Vei învăța mai multe despre moștenire în capitolul Moștenire) |
| `abstract` | Clasa nu poate fi folosită pentru a crea obiecte (Pentru a accesa o clasă abstractă, aceasta trebuie să fie moștenită de la o altă clasă. Vei învăța mai multe despre moștenire și abstractizare

### Pentru atribute, metode si constructori putem folosii urmatoarele:

| Modifier    | Descriere                                           |
|-------------|-----------------------------------------------------|
| `final`       | Atributele și metodele nu pot fi suprascrise/modificate |
| `static`      | Atributele și metodele aparțin clasei, nu unui obiect |
| `abstract`    | Poate fi folosit doar într-o clasă abstractă și doar pe metode. Metoda nu are un corp, de exemplu abstract void run();. Corpul este furnizat de subclasă (moștenit). Vei învăța mai multe despre moștenire și abstractizare în capitolele Moștenire și Abstractizare |
| `transient`   | Atributele și metodele sunt omise atunci când se serializează obiectul care le conține |
| `synchronized` | Metodele pot fi accesate doar de către un singur fir la un moment dat |
| `volatile`    | Valoarea unui atribut nu este memorată local pentru fir și este citită întotdeauna din "memoria principală" |

## `Final`

Dacă nu dorești posibilitatea de a suprascrie valorile existente ale atributelor, declară-le ca `final`:


```java
public class Main {
  final int x = 10;
  final double PI = 3.14;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 50; // will generate an error: cannot assign a value to a final variable
    myObj.PI = 25; // will generate an error: cannot assign a value to a final variable
    System.out.println(myObj.x);
  }
}

output:
Main.java:7: error: cannot assign a value to final variable x
    myObj.x = 50;
         ^
Main.java:8: error: cannot assign a value to final variable PI
    myObj.PI = 25;
         ^ 2 errors
```

## `Static`

O metodă statică înseamnă că poate fi accesată fără a crea un obiect al clasei, spre deosebire de public:


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
  public static void main(String[ ] args) {
    myStaticMethod(); // Call the static method
    // myPublicMethod(); This would output an error

    Main myObj = new Main(); // Create an object of Main
    myObj.myPublicMethod(); // Call the public method
  }
}

output:
Static methods can be called without creating objects
Public methods must be called by creating objects
```

## `Abstract`

O metodă abstractă aparține unei clase `abstracte` și nu are un corp. Corpul este furnizat de către subclasă:

```java
// Code from filename: Main.java
// abstract class
abstract class Main {
  public String fname = "John";
  public int age = 24;
  public abstract void study(); // abstract method
}

// Subclass (inherit from Main)
class Student extends Main {
  public int graduationYear = 2018;
  public void study() { // the body of the abstract method is provided here
    System.out.println("Studying all day long");
  }
}
// End code from filename: Main.java

// Code from filename: Second.java
class Second {
  public static void main(String[] args) {
    // create an object of the Student class (which inherits attributes and methods from Main)
    Student myObj = new Student();

    System.out.println("Name: " + myObj.fname);
    System.out.println("Age: " + myObj.age);
    System.out.println("Graduation Year: " + myObj.graduationYear);
    myObj.study(); // call abstract method
  }
}

output:
Name: John
Age: 24
Graduation Year: 2018
Studying all day long
```








