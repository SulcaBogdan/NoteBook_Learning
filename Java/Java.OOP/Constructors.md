# Constructorul in Java

### Un constructor în Java este o metodă specială folosită pentru a inițializa obiecte. 

Constructorul este apelat atunci când un obiect al unei clase este creat. Poate fi folosit pentru a seta valori inițiale pentru atributele obiectului:

```java
// Create a Main class
public class Main {
  int x;  // Create a class attribute

  // Create a class constructor for the Main class
  public Main() {
    x = 5;  // Set the initial value for the class attribute x
  }

  public static void main(String[] args) {
    Main myObj = new Main(); // Create an object of class Main (This will call the constructor)
    System.out.println(myObj.x); // Print the value of x
  }
}

output:
5
```

Ține cont că numele constructorului trebuie să se potrivească cu numele clasei și nu poate avea un tip de returnare (cum ar fi void).

De asemenea, observă că constructorul este apelat atunci când obiectul este creat.

**Toate clasele au constructori în mod implicit: dacă nu creezi un constructor de clasă tu însuți, Java creează unul pentru tine. Cu toate acestea, nu vei putea să setezi valori inițiale pentru atributele obiectului în acest caz.**

## Parametrii Constuctorului

Constructorii pot, de asemenea, să primească parametri, care sunt folosiți pentru a inițializa atributele.

Următorul exemplu adaugă un parametru `int y` constructorului. În interiorul constructorului setăm `x` la `y` (x=y). Când apelăm constructorul, transmitem un parametru constructorului (`5`), care va seta valoarea lui `x` la `5`:

```java
public class Main {
  int x;

  public Main(int y) {
    x = y;
  }

  public static void main(String[] args) {
    Main myObj = new Main(5);
    System.out.println(myObj.x);
  }
}

output:
5
```

Putem adauga cati parametrii dorim.

```java
public class Main {
  int modelYear;
  String modelName;

  public Main(int year, String name) {
    modelYear = year;
    modelName = name;
  }

  public static void main(String[] args) {
    Main myCar = new Main(1969, "Mustang");
    System.out.println(myCar.modelYear + " " + myCar.modelName);
  }
}

Output:
1969 Mustang
```




