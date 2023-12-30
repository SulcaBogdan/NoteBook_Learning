# Wrapper Classes in Java

Clasele wrapper oferă o modalitate de a utiliza tipuri de date primitive (`int`, `boolean`, etc.) ca obiecte.

Tabelul de mai jos arată tipul primitiv și clasa wrapper echivalentă:

Tip de date primitiv | Clasa wrapper
--------------------- | ---------------
byte                  | Byte
short                | Short
int                  | Integer
long                 | Long
float                | Float
double               | Double
boolean              | Boolean
char                 | Character

Uneori trebuie să folosești clasele wrapper, de exemplu atunci când lucrezi cu obiecte de colecție, cum ar fi ArrayList, unde tipurile primitive nu pot fi utilizate (lista poate stoca doar obiecte):

```java
ArrayList<int> myNumbers = new ArrayList<int>(); // Invalid
```

```java
ArrayList<Integer> myNumbers = new ArrayList<Integer>(); // Valid
```

## Crearea unui wrapper class

Pentru a crea un obiect wrapper, utilizează clasa wrapper în locul tipului primitiv. Pentru a obține valoarea, poți doar să afișezi obiectul:

```java
public class Main {
  public static void main(String[] args) {
    Integer myInt = 5;
    Double myDouble = 5.99;
    Character myChar = 'A';
    System.out.println(myInt);
    System.out.println(myDouble);
    System.out.println(myChar);
  }
}

output:
5
5.99
A
```

Deoarece lucrezi acum cu obiecte, poți utiliza anumite metode pentru a obține informații despre obiectul specific.

De exemplu, următoarele metode sunt utilizate pentru a obține valoarea asociată obiectului wrapper corespunzător: `intValue()`, `byteValue()`, `shortValue()`, `longValue()`, `floatValue()`, `doubleValue()`, `charValue()`, `booleanValue()`.

Acest exemplu va afișa același rezultat ca și exemplul de mai sus:


```java
public class Main {
  public static void main(String[] args) {
    Integer myInt = 5;
    Double myDouble = 5.99;
    Character myChar = 'A';
    System.out.println(myInt.intValue());
    System.out.println(myDouble.doubleValue());
    System.out.println(myChar.charValue());
  }
}

output:
5
5.99
A
```

O altă metodă utilă este metoda `toString()`, care este utilizată pentru a converti obiectele wrapper în șiruri de caractere.

În exemplul următor, convertim un `Integer` într-un șir de caractere și utilizăm metoda `length()` a clasei `String` pentru a afișa lungimea "șirului":

```java
public class Main {
  public static void main(String[] args) {
    Integer myInt = 100;
    String myString = myInt.toString();
    System.out.println(myString.length());
  }
}

output:
3
```


