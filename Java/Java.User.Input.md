# Cititul de la tastatura (User input) in Java

Clasa `Scanner` este folosită pentru a obține input de la utilizator și se găsește în pachetul `java.util`.

Pentru a folosi clasa `Scanner`, creează un obiect al clasei și folosește oricare dintre metodele disponibile găsite în documentația clasei `Scanner`. În exemplul nostru, vom folosi metoda `nextLine()`, care este folosită pentru a citi șiruri de caractere (`Strings`):


```java
import java.util.Scanner;  // Import the Scanner class

class Main {
  public static void main(String[] args) {
    Scanner myObj = new Scanner(System.in);  // Create a Scanner object
    System.out.println("Enter username");

    String userName = myObj.nextLine();  // Read user input
    System.out.println("Username is: " + userName);  // Output user input
  }
}

Process:
Enter username
Dodan

output:
Username is: Dodan
```

## Tipurile de input


În exemplul de mai sus, am folosit metoda `nextLine()`, care este utilizată pentru a citi șiruri de caractere (Strings). Pentru a citi alte tipuri, uită-te la tabelul de mai jos:

| Metodă          | Descriere                                       |
| --------------- | ----------------------------------------------- |
| `nextBoolean()`   | Citește o valoare booleană de la utilizator      |
| `nextByte()`      | Citește o valoare byte de la utilizator          |
| `nextDouble()`    | Citește o valoare double de la utilizator        |
| `nextFloat()`     | Citește o valoare float de la utilizator         |
| `nextInt()`       | Citește o valoare int de la utilizator           |
| `nextLine()`      | Citește o valoare String de la utilizator        |
| `nextLong()`      | Citește o valoare long de la utilizator          |
| `nextShort()`     | Citește o valoare short de la utilizator         |


În exemplul de mai jos, folosim diferite metode pentru a citi date de diferite tipuri:

```java
import java.util.Scanner;

class Main {
  public static void main(String[] args) {
    Scanner myObj = new Scanner(System.in);

    System.out.println("Enter name, age and salary:");

    // String input
    String name = myObj.nextLine();

    // Numerical input
    int age = myObj.nextInt();
    double salary = myObj.nextDouble();

    // Output input by user
    System.out.println("Name: " + name);
    System.out.println("Age: " + age);
    System.out.println("Salary: " + salary);
  }
}

process:
Enter name, age and salary:
Dodan
25
5999

output:
Name: Dodan
Age: 25
Salary: 5999
```

Notă: Dacă introduci un input greșit (de exemplu, text într-un câmp destinat numerelor), vei primi o excepție/eroare (cum ar fi `InputMismatchException`).
