# Encapsulation sau Incapsularea in Java OOP

**Înțelesul încapsulării este de a te asigura că datele "sensibile" sunt ascunse de utilizatori. Pentru a realiza acest lucru, trebuie să:**

- Declare variabilele/atributele clasei ca private
- Furnizați metode publice get și set pentru a accesa și actualiza valoarea unei variabile private

## Getter si Setter

Ai învățat din capitolul anterior că variabilele private pot fi accesate doar în cadrul aceleiași clase (o clasă externă nu are acces la ele). Cu toate acestea, este posibil să le accesăm dacă furnizăm metode publice `get` și `set`.

Metoda `get` returnează valoarea variabilei, iar metoda `set` o setează.

Sintaxa pentru ambele este că încep cu `get` sau `set`, urmate de numele variabilei, cu prima literă în majusculă:

```java
public class Person {
  private String name; // private = restricted access

  // Getter
  public String getName() {
    return name;
  }

  // Setter
  public void setName(String newName) {
    this.name = newName;
  }
}
```

**Exemplu explicat**

Metoda `get` returnează valoarea variabilei `name`.

Metoda `set` primește un parametru (`newName`) și îl atribuie variabilei `name`. Cuvântul cheie `this` este folosit pentru a se referi la obiectul curent.

Cu toate acestea, deoarece variabila name este declarată ca privată, nu o putem accesa din afara acestei clase:

```java
public class Main {
  public static void main(String[] args) {
    Person myObj = new Person();
    myObj.name = "John";  // error
    System.out.println(myObj.name); // error 
  }
}

output:
Main.java:4: error: name has private access in Person
    myObj.name = "John";
         ^
Main.java:5: error: name has private access in Person
    System.out.println(myObj.name);
                  ^
2 errors
```

Dacă variabila ar fi fost declarată ca publică, ne-am aștepta la următoarea ieșire:

```
output:
John
```

În schimb, folosim metodele `getName()` și `setName()` pentru a accesa și actualiza variabila:


```java
public class Main {
  public static void main(String[] args) {
    Person myObj = new Person();
    myObj.setName("John"); // Set the value of the name variable to "John"
    System.out.println(myObj.getName());
  }
}

output:
John
```


## De ce Incapsularea?

- Mai bun control al atributelor și metodelor clasei
- Atributele clasei pot fi făcute doar-citire (dacă folosești doar metoda get) sau doar-scriere (dacă folosești doar metoda set)
- Flexibilitate: programatorul poate schimba o parte a codului fără a afecta alte părți
- Creșterea securității datelor


