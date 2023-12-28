# Valorile Numerice in Java

## Numere

Tipurile primitive de numere sunt împărțite în două categorii:

### Tipuri intregi

Stochează numere întregi, pozitive sau negative (cum ar fi 123 sau -456), fără zecimale. Tipurile valabile sunt byte, short, int și long. Tipul pe care ar trebui să-l folosești depinde de valoarea numerică.

### Tipuri cu Punct Flotant

Reprezintă numere cu o parte fracționară, care conține una sau mai multe zecimale. Există două tipuri: float și double.

Chiar dacă există multe tipuri numerice în Java, cele mai folosite pentru numere sunt int (pentru numere întregi) și double (pentru numere cu virgulă mobilă). Cu toate acestea, le vom descrie pe toate pe măsură ce continui să citești.

## Integer

### Byte

Tipul de date `byte` poate stoca numere întregi de la -128 la 127. Acesta poate fi folosit în locul tipului int sau altor tipuri întregi pentru a economisi memorie atunci când ești sigur că valoarea se va afla în intervalul -128 și 127:

```java
byte myNum = 100;
System.out.println(myNum);

output:
100
```

### Short

Tipul de date `short` poate stoca numere întregi de la `-32,768` la `32,767`:

```java
short myNum = 5000;
System.out.println(myNum);

output:
5000
```

### Int

Tipul de date `int` poate stoca numere întregi de la `-2,147,483,648` la `2,147,483,647`. În general, și în tutorialul nostru, tipul de date int este tipul preferat atunci când cream variabile cu o valoare numerică.

```java
int myNum = 100000;
System.out.println(myNum);

output:
100000
```

### Long

Tipul de date `long` poate stoca numere întregi de la `-9,223,372,036,854,775,808` la `9,223,372,036,854,775,807`. Acesta este folosit atunci când tipul de date int nu este suficient de mare pentru a stoca valoarea. Notă: Ar trebui să închei valoarea cu `"L"`:

```java
long myNum = 15000000000L;
System.out.println(myNum);

output:
15000000000
```

### Floating point 

Ar trebui să folosești un tip de punct flotant ori de câte ori ai nevoie de un număr cu zecimale, cum ar fi `9.99` sau `3.14515`.

Tipurile de date `float` și `double` pot stoca numere `fracționare`. Notă: Ar trebui să închei valoarea cu `"f"` pentru float-uri și `"d"` pentru double-uri:

```java
float myNum = 5.75f;
System.out.println(myNum);

output:
5.75
```

```java
double myNum = 19.99d;
System.out.println(myNum);

output:
19.99
```

### Utilizare float sau double?

Precizia unei valori `float` indică câte cifre poate avea valoarea după punctul zecimal. Precizia float-ului este de doar `șase` sau `șapte` cifre zecimale, în timp ce variabilele `double` au o precizie de aproximativ 15 cifre. Prin urmare, este mai sigur să folosești double pentru cele mai multe calculații.

### Numere Științifice

Un număr cu virgulă mobilă poate fi și un număr științific cu un `"e"` pentru a indica puterea lui 10:

```java
float f1 = 35e3f;
double d1 = 12E4d;
System.out.println(f1);
System.out.println(d1);

output:
35000.0
120000.0
```

