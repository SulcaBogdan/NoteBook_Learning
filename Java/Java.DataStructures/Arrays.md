# Arrays in Java

## Arrays în Java

Arrays sunt folosite pentru a stoca mai multe valori într-o singură variabilă, în loc să declari variabile separate pentru fiecare valoare.

Pentru a declara un array, definește tipul de variabilă cu paranteze pătrate:

```java
String[] cars;
```

## Inițializarea unui array în Java

Am declarat acum o variabilă care conține un array de șiruri de caractere. Pentru a introduce valori în el, poți plasa valorile într-o listă separată prin virgule, în interiorul acoladelor:

```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
```

Daca vrem sa cream un array de numere putem scrie asa:

```java
int[] myNum = {1,2,3,4,5};
```

## Accesarea elementelor unui array în Java

Poți accesa un element al unui array referindu-te la numărul de index.

Această declarație accesează valoarea primului element din array-ul "cars":

```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
System.out.println(cars[0]);

output:
Volvo
```

### Notă: Indexele array-urilor încep cu 0: [0] este primul element. [1] este al doilea element, etc.

### Modificarea unui element al unui array în Java

Pentru a schimba valoarea unui element specific, referă-te la numărul de index:
```java
cars[0] = "Toyota";
```

```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
cars[0] = "Toyota";
System.out.println(cars[0]);

output:
Toyota
```

### Lungimea unui array în Java

Pentru a afla câte elemente are un array, folosește proprietatea length:
```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
System.out.println(cars.length);

output:
4
```

# Parcurgerea unui array în Java

Poți parcurge elementele array-ului cu ajutorul buclei `for`, folosind proprietatea length pentru a specifica de câte ori trebuie să ruleze bucla.

Exemplul de mai jos afișează toate elementele din array-ul "cars":

```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (int i = 0; i < cars.length; i++) {
  System.out.println(cars[i]);
}

output:
Volvo
BMW
Ford
Mazda
```

## Parcurgerea unui array cu bucla "for-each" în Java

Există și o buclă "for-each" care este folosită exclusiv pentru a parcurge elementele din array-uri:


```java
for (type variable : arrayname) {
  ...
}
```

### Parcurgerea unui array cu bucla "for-each" în Java

Exemplul de mai jos afișează toate elementele din array-ul "cars" folosind bucla "for-each":

```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (String i : cars) {
  System.out.println(i);
}

output:
Volvo
BMW
Ford
Mazda
```


Exemplul de mai sus poate fi citit astfel: pentru fiecare element String (numit `i` - ca index) din "`cars`", afișează valoarea lui `i`.

Dacă compari bucla "for" cu bucla "for-each", vei observa că metoda "for-each" este mai ușor de scris, nu necesită un contor (folosind proprietatea length), și este mai ușor de citit.

# Array-uri Multidimensionale în Java

Un array multidimensional este un array de array-uri.

Array-urile multidimensionale sunt utile atunci când vrei să stochezi date sub formă tabulară, ca o tabelă cu rânduri și coloane.

Pentru a crea un array bidimensional, adaugă fiecare array în propriul set de acolade:

```java
int[][] myNumbers = { {1, 2, 3, 4}, {5, 6, 7} };
```

### Accesarea Elementelor

Pentru a accesa elementele array-ului `myNumbers`, specifică două indecși: unul pentru array și unul pentru elementul din interiorul acelui array. Acest exemplu accesează al treilea element (2) din al doilea array (1) din `myNumbers`:

```java
int[][] myNumbers = { {1, 2, 3, 4}, {5, 6, 7} };
System.out.println(myNumbers[1][2]);

output:
7
```

### Rețineți că:

Indecșii array-ului încep cu 0: [0] este primul element. [1] este al doilea element, etc.


```java
int[][] myNumbers = { {1, 2, 3, 4}, {5, 6, 7} };
myNumbers[1][2] = 9;
System.out.println(myNumbers[1][2]); 

output:
9
```

### Parcurgerea unui array multidimensional

Putem folosi, de asemenea, un for loop în interiorul altui for loop pentru a obține elementele unui tablou bidimensional (încă trebuie să indicăm cele două indexuri):


```java
public class Main {
  public static void main(String[] args) {
    int[][] myNumbers = { {1, 2, 3, 4}, {5, 6, 7} };
    for (int i = 0; i < myNumbers.length; ++i) {
      for(int j = 0; j < myNumbers[i].length; ++j) {
        System.out.println(myNumbers[i][j]);
      }
    }
  }
}

output:
1
2
3
4
5
6
7
```

