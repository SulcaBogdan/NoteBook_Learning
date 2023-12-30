# Interfetele in Java

O altă modalitate de a realiza abstractizarea în Java este cu ajutorul interfețelor.

O interfață este o "clasă complet abstractă" care este folosită pentru a grupa metodele corelate cu corpuri goale:


```java
// interface
interface Animal {
  public void animalSound(); // interface method (does not have a body)
  public void run(); // interface method (does not have a body)
}
```

Pentru a accesa metodele interfeței, interfața trebuie să fie "implementată" (ceva asemănător cu moștenirea) de către o altă clasă cu ajutorul cuvântului cheie `implements` (în loc de `extends`). Corpul metodei interfeței este furnizat de către clasa "implementată":

```java
// Interface
interface Animal {
  public void animalSound(); // interface method (does not have a body)
  public void sleep(); // interface method (does not have a body)
}

// Pig "implements" the Animal interface
class Pig implements Animal {
  public void animalSound() {
    // The body of animalSound() is provided here
    System.out.println("The pig says: wee wee");
  }
  public void sleep() {
    // The body of sleep() is provided here
    System.out.println("Zzz");
  }
}

class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig();  // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}

output:
The pig says: wee wee
Zzz
```

### Note despre Interfețe:
- La fel ca și clasele abstracte, interfețele nu pot fi folosite pentru a crea obiecte (în exemplul de mai sus, nu este posibil să se creeze un obiect "`Animal`" în `MyMainClass`)
- Metodele interfeței nu au un corp - corpul este furnizat de clasa "implementată"
- La implementarea unei interfețe, trebuie să suprascrii toate metodele sale
- Metodele interfeței sunt, în mod implicit, abstracte și publice
- Atributele interfeței sunt, în mod implicit, `publice`, `statice` și `finale`
- O interfață nu poate conține un `constructor` (deoarece nu poate fi folosită pentru a crea obiecte)
  
### De ce și când să folosim Interfețe?
1) Pentru a realiza securitatea - ascunde anumite detalii și arată doar detaliile importante ale unui obiect (interfață).

2) Java nu suportă "moștenirea multiplă" (o clasă poate moșteni doar de la o superclasă). Cu toate acestea, poate fi realizată cu ajutorul interfețelor, deoarece clasa poate implementa mai multe interfețe. Notă: Pentru a implementa mai multe interfețe, le separi cu o virgulă (vezi exemplul de mai jos).

## Implementarea a mai multor interfete 

```java
interface FirstInterface {
  public void myMethod(); // interface method
}

interface SecondInterface {
  public void myOtherMethod(); // interface method
}

class DemoClass implements FirstInterface, SecondInterface {
  public void myMethod() {
    System.out.println("Some text..");
  }
  public void myOtherMethod() {
    System.out.println("Some other text...");
  }
}

class Main {
  public static void main(String[] args) {
    DemoClass myObj = new DemoClass();
    myObj.myMethod();
    myObj.myOtherMethod();
  }
}

output:
Some text...
Some other text...
```