# Lambda in Java

`Lambda` expressions în Java 8 permit programatorilor să scrie expresii scurte și concize. Este o modalitate simplă de a defini funcții anonime, adică funcții fără un nume.

De exemplu, în loc să scrii o clasă întreagă pentru a implementa o interfață funcțională (o interfață cu o singură metodă), poți folosi o expresie lambda pentru a defini acea metodă într-o linie sau două de cod. Este un mod mai concis și mai expresiv de a scrie cod.

# Syntaxa

```java
parameter -> expression
```

Pentru a folosii mai mult de un parametru , le punem in paranteza

```java
(parameter1, parameter2) -> expression
```

Expresiile sunt limitate. Trebuie să returneze imediat o valoare și nu pot conține variabile, asignări sau instrucțiuni precum `if` sau `for`. Pentru operații mai complexe, poți folosi un bloc de cod cu acolade. Dacă expresia lambda trebuie să returneze o valoare, atunci blocul de cod ar trebui să conțină o instrucțiune `return`.

```java
(parameter1, parameter2) -> { code block }
```

## Folosirea expresiilor lambda

```java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(5);
    numbers.add(9);
    numbers.add(8);
    numbers.add(1);
    numbers.forEach( (n) -> { System.out.println(n); } );
  }
}

output:
5
9
8
1
```

Expresiile `lambda` pot fi stocate în variabile dacă tipul variabilei este o interfață care are doar o singură metodă. Expresia `lambda` trebuie să aibă aceeași număr de parametri și același tip de return ca și acea metodă. Java are multe astfel de interfețe încorporate, cum ar fi interfața Consumer (găsită în pachetul `java.util`) utilizată de liste.

```java
import java.util.ArrayList;
import java.util.function.Consumer;

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(5);
    numbers.add(9);
    numbers.add(8);
    numbers.add(1);
    Consumer<Integer> method = (n) -> { System.out.println(n); };
    numbers.forEach( method );
  }
}

output:
5
9
8
1
```

Pentru a utiliza o expresie `lambda` într-o metodă, metoda ar trebui să aibă un parametru cu tipul unei interfețe cu o singură metodă. Apelarea metodei interfeței va rula expresia `lambda`:

```java
interface StringFunction {
  String run(String str);
}

public class Main {
  public static void main(String[] args) {
    StringFunction exclaim = (s) -> s + "!";
    StringFunction ask = (s) -> s + "?";
    printFormatted("Hello", exclaim);
    printFormatted("Hello", ask);
  }
  public static void printFormatted(String str, StringFunction format) {
    String result = format.run(str);
    System.out.println(result);
  }
}

output:
Hello!
Hello?
```