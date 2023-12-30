# Polymorphism sau Polimorfismul in Java OOP

Polimorfismul înseamnă "multe forme" și apare atunci când avem mai multe clase care sunt legate între ele prin moștenire.

Așa cum am specificat în capitolul anterior, moștenirea ne permite să moștenim atribute și metode de la o altă clasă. Polimorfismul folosește acele metode pentru a îndeplini sarcini diferite. Acest lucru ne permite să realizăm o singură acțiune în moduri diferite.

De exemplu, gândește-te la o superclasă numită `Animal` care are o metodă numită `animalSound()`. Subclasele Animalelor ar putea fi `Porci`, `Pisici`, `Câini`, `Păsări` - și ele au, de asemenea, propria implementare a unui sunet de animal (porcul scâncetează, pisica miaună, etc.):

```java
class Animal {
  public void animalSound() {
    System.out.println("The animal makes a sound");
  }
}

class Pig extends Animal {
  public void animalSound() {
    System.out.println("The pig says: wee wee");
  }
}

class Dog extends Animal {
  public void animalSound() {
    System.out.println("The dog says: bow wow");
  }
}
```

Acum putem crea obiecte de tip `Pig` și `Dog` și să apelăm metoda `animalSound()` pe ambele:


```java
class Animal {
  public void animalSound() {
    System.out.println("The animal makes a sound");
  }
}

class Pig extends Animal {
  public void animalSound() {
    System.out.println("The pig says: wee wee");
  }
}

class Dog extends Animal {
  public void animalSound() {
    System.out.println("The dog says: bow wow");
  }
}

class Main {
  public static void main(String[] args) {
    Animal myAnimal = new Animal();  // Create a Animal object
    Animal myPig = new Pig();  // Create a Pig object
    Animal myDog = new Dog();  // Create a Dog object
    myAnimal.animalSound();
    myPig.animalSound();
    myDog.animalSound();
  }
}

output:
The animal makes a sound
The pig says: wee wee
The dog says: bow wow
```

