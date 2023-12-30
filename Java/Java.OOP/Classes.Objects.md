# Clasele si Obiectele in Java

Java este un limbaj de programare orientat pe obiect.

Totul în Java este asociat cu **clase** și **obiecte**, împreună cu atributele și metodele lor. 

De exemplu, în viața reală, o mașină este un obiect. Mașina are atribute, cum ar fi greutatea și culoarea, și metode, cum ar fi a conduce și a frâna.

O clasă este ca un constructor de obiect sau un "proiect" pentru crearea obiectelor.

## Crearea unei clase in Java

Pentru a crea o clasa in Java folosim cuvantul cheie `class`:

```java
public class Main{
    int x = 5;
}
```

## Crearea unui obiect in Java

În Java, un obiect este creat dintr-o clasă. Noi am creat deja clasa numită `Main`, așa că acum putem folosi asta pentru a crea obiecte.

Pentru a crea un obiect `Main`, specificați numele clasei, urmat de numele obiectului și utilizați cuvântul cheie `new`:

```java
public class Main{
    int x = 5;

    public static void main(String[] args){
        Main myObj = new Main();
        System.out.println(myObj.x);
    }
}

output:
5
```

## Obiecte multiple

```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main myObj1 = new Main();  // Object 1
    Main myObj2 = new Main();  // Object 2
    System.out.println(myObj1.x);
    System.out.println(myObj2.x);
  }
}

output:
5
5
```

## Utilizarea a mai multor clase

Poți, de asemenea, să creezi un obiect al unei clase și să-l accesezi într-o altă clasă. Aceasta este adesea folosită pentru o mai bună organizare a claselor (o clasă are toate atributele și metodele, în timp ce cealaltă clasă conține metoda `main()` (codul de executat)).

Ține minte că numele fișierului Java ar trebui să se potrivească cu numele clasei. În acest exemplu, am creat două fișiere în același director/folder:

Main.java
Second.java

```java
public class Main {
  int x = 5;
}
```

```java
class Second {
  public static void main(String[] args) {
    Main myObj = new Main();
    System.out.println(myObj.x);
  }
}

output:
5
```




