# Abstraction sau Abstractizarea in Java OOP

### Clase și Metode Abstracte
Abstractizarea datelor este procesul de ascundere a anumitor detalii și prezentare doar a informațiilor esențiale utilizatorului.
Abstractizarea poate fi realizată fie cu clase abstracte, fie cu interfețe (despre care vei afla mai multe în capitolul următor).

Cuvântul cheie `abstract` este un modificator non-acces, folosit pentru clase și metode:

Clasă abstractă: este o clasă restricționată care nu poate fi folosită pentru a crea obiecte (pentru a o accesa, trebuie să fie moștenită de la o altă clasă).

Metodă abstractă: poate fi folosită doar într-o clasă abstractă și nu are un corp. Corpul este furnizat de către subclasă (moștenit).

O clasă abstractă poate avea atât metode abstracte, cât și metode regulate:

```java
abstract class Animal {
  public abstract void animalSound();
  public void sleep() {
    System.out.println("Zzz");
  }
}
```

Din exemplul de mai sus, nu este posibil să se creeze un obiect al clasei `Animal`:

```
Animal myObj = new Animal(); // will generate an error
```

```java
// Abstract class
abstract class Animal {
  // Abstract method (does not have a body)
  public abstract void animalSound();
  // Regular method
  public void sleep() {
    System.out.println("Zzz");
  }
}

// Subclass (inherit from Animal)
class Pig extends Animal {
  public void animalSound() {
    // The body of animalSound() is provided here
    System.out.println("The pig says: wee wee");
  }
}

class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig(); // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}

output:
The pig says: wee wee
Zzz
```
### De ce și când să folosim Clase și Metode Abstracte?
- Pentru a realiza securitatea - ascunde anumite detalii și arată doar detaliile importante ale unui obiect.

`Notă`: Abstractizarea poate fi realizată și cu ajutorul Interfețelor, despre care vei afla mai multe în capitolul următor.


