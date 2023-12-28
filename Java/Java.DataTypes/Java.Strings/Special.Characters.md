# Caracterele speciale 

### Caractere Speciale în Șiruri

Deoarece șirurile trebuie scrise între ghilimele, Java va înțelege greșit acest șir și va genera o eroare

```java
String txt = "We are the so-called "Vikings" from the north.";
```

Soluția pentru a evita această problemă este să folosești caracterul de scăpare cu bara oblică inversă `(\)`.

Caracterul de scăpare cu bara oblică inversă `(\)` transformă caracterele speciale în caractere de șir.

| Caracter de Scăpare | Rezultat | Descriere                |
|----------------------|----------|--------------------------|
| `\'`                   | '        | Apostrof                 |
| `\"`                   | "        | Ghilimele duble          |
|` \\ `                  | \        | Bară oblică inversă      |

Secvența `\"` introduce o ghilimea dublă într-un șir:

```java
String txt = "We are the so-called \"Vikings\" from the north.";
```

Secvența `\'` introduce un apostrof într-un șir:

```java
String txt = "It\'s alright.";
```

Secvența \\ introduce o bară oblică inversă într-un șir:


```java
String txt = "The character \\ is called backslash.";
```

| Cod   | Rezultat         |
|-------|------------------|
| \n    | Nouă Linie       |
| \r    | Întoarcere        |
| \t    | Tab              |
| \b    | Backspace        |
| \f    | Avans Pagină     |
