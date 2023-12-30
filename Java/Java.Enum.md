# Enumeratiile in Java

Un `enum` este o "clasă" specială care reprezintă un grup de constante (variabile neschimbabile, precum variabilele finale).

Pentru a crea un `enum`, folosește cuvântul cheie `enum` (în loc de `class` sau `interface`) și separă constantele cu o virgulă. Observă că acestea trebuie să fie scrise cu litere majuscule:

```java
enum Level {
  LOW,
  MEDIUM,
  HIGH
}
```

Putem accesa constantele astfel:

```java
Level.LOW
Level.MEDIUM
Level.HIGH
```

### Enum este prescurtarea pentru "enumerări", care înseamnă "listate în mod specific".


## Enum in interiorul unei clase

```java
public class Main {
  enum Level {
    LOW,
    MEDIUM,
    HIGH
  }

  public static void main(String[] args) {
    Level myVar = Level.MEDIUM; 
    System.out.println(myVar);
  }
}

output:
MEDIUM
```

## Enum in Switch statement

Enum-urile sunt adesea folosite în instrucțiuni switch pentru a verifica valorile corespunzătoare:

```java
enum Level {
  LOW,
  MEDIUM,
  HIGH
}

public class Main {
  public static void main(String[] args) {
    Level myVar = Level.MEDIUM;

    switch(myVar) {
      case LOW:
        System.out.println("Low level");
        break;
      case MEDIUM:
         System.out.println("Medium level");
        break;
      case HIGH:
        System.out.println("High level");
        break;
    }
  }
}

output:
Medium level
```

## Parcurgerea unui Enum

Tipul `enum` are o metodă `values()`, care returnează un array al tuturor constantelor `enum`. Această metodă este utilă atunci când dorești să parcurgi constantele unui `enum`:


```java
for (Level myVar : Level.values()) {
  System.out.println(myVar);
}

output:
LOW
MEDIUM
HIGH
```

### Diferența dintre Enum-uri și Clase

Un `enum` poate, la fel ca o clasă, să aibă atribute și metode. Singura diferență este că constantele enum sunt `publice`, `statice` și `finale` (neschimbabile - nu pot fi suprascrise).

Un `enum` nu poate fi folosit pentru a crea obiecte și nu poate extinde alte clase (dar poate implementa interfețe).

### De ce și când să folosim Enum-uri?
Folosește enum-urile atunci când ai valori pe care știi că nu se vor schimba, precum zilele lunii, zilele săptămânii, culorile, un set de cărți etc.





