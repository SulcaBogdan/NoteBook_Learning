# Inheritance sau Mostenirea in Java OOP

### Moștenirea în Java (Subclasă și Superclasă)
În Java, este posibil să moștenești atribute și metode de la o clasă la alta. Grupăm conceptul de "moștenire" în două categorii:

- `subclasă` (copil) - clasa care moștenește de la o altă clasă
- `superclasă` (părinte) - clasa care este moștenită
Pentru a moșteni de la o clasă, folosește cuvântul cheie `extends`.

În exemplul de mai jos, clasa Car (subclasă) moștenește atributele și metodele clasei Vehicle (superclasă):

```java
class Vehicle {
  protected String brand = "Ford";        // Vehicle attribute
  public void honk() {                    // Vehicle method
    System.out.println("Tuut, tuut!");
  }
}

class Car extends Vehicle {
  private String modelName = "Mustang";    // Car attribute
  public static void main(String[] args) {

    // Create a myCar object
    Car myCar = new Car();

    // Call the honk() method (from the Vehicle class) on the myCar object
    myCar.honk();

    // Display the value of the brand attribute (from the Vehicle class) and the value of the modelName from the Car class
    System.out.println(myCar.brand + " " + myCar.modelName);
  }
}

output:
Tuut, tuut!
Ford Mustang
```
Ai observat modificatorul `protected` în clasa `Vehicle`?

Am setat atributul `brand` în clasa `Vehicle` cu un modificator de acces `protected`. Dacă ar fi fost setat la `private`, clasa `Car` nu ar putea să-l acceseze.

**De ce și când să folosim "Moștenirea"?**
- Este utilă pentru reutilizarea codului: reutilizează atributele și metodele unei clase existente atunci când creezi o clasă nouă.

## Cuvântul cheie `final`
Dacă nu dorești ca alte clase să moștenească de la o clasă, folosește cuvântul cheie `final`:


```java
final class Vehicle {
  ...
}

class Car extends Vehicle {
  ...
}
```

```
output:
Main.java:9: error: cannot inherit from final Vehicle
class Main extends Vehicle {
                  ^
1 error)
```

