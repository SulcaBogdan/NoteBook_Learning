# Variabilele in Java

# Variabile în Java

Variabilele sunt containere pentru stocarea valorilor datelor.

În Java, există diferite tipuri de variabile, de exemplu:

1. **String:**
   - Stochează texte, cum ar fi "Hello".
   - Valorile de tip String sunt înconjurate de ghilimele duble.

    ```java
    String nume = "John";
    ```

2. **int:**
   - Stochează numere întregi (numere întregi), fără zecimale, cum ar fi 123 sau -123.

    ```java
    int varsta = 25;
    ```

3. **float:**
   - Stochează numere cu virgulă mobilă, cu zecimale, cum ar fi 19.99 sau -19.99.
   - Notă: Litera "f" de la sfârșit indică faptul că valoarea este de tip float.

    ```java
    float pret = 19.99f;
    ```

4. **char:**
   - Stochează caractere unice, cum ar fi 'a' sau 'B'.
   - Valorile de tip char sunt înconjurate de ghilimele simple.

    ```java
    char litera = 'A';
    ```

5. **boolean:**
   - Stochează valori cu două stări: adevărat sau fals.

    ```java
    boolean esteAdevărat = true;
    ```

## Declararea (Crearea) Variabilelor

Pentru a crea o variabilă, trebuie să specificați tipul și să-i atribuiți o valoare:

```java
type variableName = value;
```

Aici, `type` este unul dintre tipurile Java (cum ar fi `int` sau `String`), iar `variableName` este numele variabilei (cum ar fi `x` sau `name`). Semnul egal este folosit pentru a atribui valori variabilei.

### Exemplu de Variabilă Text
```java
String name = "John";
System.out.println(name);

output:
John
```

### Exemplu de Variabilă Numerică
```java
int myNum = 15;
System.out.println(myNum);

output:
15
```

### Poți, de asemenea, să declari o variabilă fără a-i atribui valoarea și să-i atribui valoarea mai târziu:

#### Exemplu de Declarație Anterioră
```java
int myNum;
myNum = 15;
System.out.println(myNum);

output:
15
```

Observă că dacă atribui o valoare nouă unei variabile existente, aceasta va **suprascrie** valoarea anterioară:

#### Exemplu de Suprascriere a Valorii
```java
int myNum = 15;
myNum = 20;  // myNum este acum 20
System.out.println(myNum);

output:
20
```

## Variabile Finale

Dacă nu dorești ca alții (sau chiar tu însuți) să suprascrie valori existente, folosește cuvântul cheie `final` (aceasta va declara variabila ca "finală" sau "constantă", ceea ce înseamnă că nu poate fi schimbată și este doar pentru citire):

### Exemplu

```java
final int myNum = 15;
myNum = 20;  // va genera o eroare: nu se poate atribui o valoare unei variabile finale

output:
Main.java:4: error: cannot assign a value to final variable myNum
    myNum = 20;
         ^
1 error
```

## Alte Tipuri de Variabile
O demonstrație despre cum să declari variabile de alte tipuri:

```java
int myNum = 5;
float myFloatNum = 5.99f;
char myLetter = 'D';
boolean myBool = true;
String myText = "Hello";
```

## Afișarea Variabilelor

Metoda `println()` este adesea folosită pentru a afișa variabile.

Pentru a combina atât textul cât și o variabilă, folosește caracterul +:

### Exemplu

```java
String name = "John";
System.out.println("Hello " + name);

output:
Hello John
```
Poți, de asemenea, să folosești caracterul + pentru a adăuga o variabilă la alta


### Exemplu

```java
String firstName = "John ";
String lastName = "Doe";
String fullName = firstName + lastName;
System.out.println(fullName);

output:
John Doe
```

Pentru valori numerice, caracterul + funcționează ca un operator matematic (observă că folosim variabile int (integer) aici):

### Exemplu

```java
int x = 5;
int y = 6;
System.out.println(x + y); // Afișează valoarea lui x + y

output:
11
```

Din exemplul de mai sus, te poți aștepta ca:

- `x` să stocheze valoarea `5`
- `y` să stocheze valoarea `6`
Apoi folosim metoda `println()` pentru a afișa valoarea lui `x + y`, care este `11`.

## Declararea a Mai Multor Variabile

Pentru a declara mai multe variabile de același tip, poți utiliza o listă separată prin virgulă:

### Exemplu

În loc să scrii:

```java
int x = 5;
int y = 6;
int z = 50;
System.out.println(x + y + z);

output:
61
```

Poți scrie pur și simplu:

```java
int x = 5, y = 6, z = 50;
System.out.println(x + y + z);

output:
61
```
O Valoare pentru Mai Multe Variabile
Poți atribui aceeași valoare mai multor variabile într-o singură linie:

```java
int x, y, z;
x = y = z = 50;
System.out.println(x + y + z);

output:
61
```

## Identificatori

Toate variabilele Java trebuie să fie identificate cu nume unice.

Aceste nume unice se numesc `identificatori`.

`Identificatorii` pot fi nume scurte (cum ar fi `x` și `y`) sau nume mai descriptive (`age`, `sum`, `totalVolume`).

**Notă:** Se recomandă utilizarea unor nume descriptive pentru a crea cod ușor de înțeles și de întreținut.

```java
// Corect
int minutesPerHour = 60;

// Este ok, dar este mai greu sa ne dam seama ce inseamna 'm'
int m = 60;
```

## Regulile Generale pentru Numele Variabilelor

Regulile generale pentru denumirea variabilelor sunt:

- Numele pot conține litere, cifre, underscore `(_)` și semnele dolarului `($)`.
- Numele trebuie să înceapă cu o literă.
- Numele ar trebui să înceapă cu o literă mică și nu poate conține spații albe.
- Numele pot începe și cu `$` și `_` (dar nu le vom folosi în acest tutorial).
- Numele sunt sensibile la majuscule și minuscule (`"myVar"` și `"myvar"` sunt variabile diferite).
- Cuvintele rezervate (cum ar fi cuvintele cheie `Java`, precum int sau boolean) nu pot fi utilizate ca nume.
