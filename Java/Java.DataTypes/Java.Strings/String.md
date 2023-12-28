# Sirurile in Java

## Șiruri de Caractere în Java

Șirurile sunt folosite pentru a stoca text.

O variabilă String conține o colecție de caractere înconjurată de ghilimele duble:

```java
String greeting = "Hello";
```

## Lungimea unui Șir de Caractere în Java

Un `String` în Java este de fapt un obiect, care conține metode care pot realiza anumite operații pe șiruri. De exemplu, lungimea unui șir poate fi găsită cu ajutorul metodei `length()`:

```java
String txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
System.out.println("Lungimea string-ului este:  " + txt.length());

output:
Lungimea string-ului este: 26
```

## Mai Multe Metode pentru Șiruri de Caractere în Java

Există multe metode pentru șiruri disponibile, de exemplu toUpperCase() și toLowerCase():

```java
String txt = "Hello World";
System.out.println(txt.toUpperCase());  
System.out.println(txt.toLowerCase());   

output:
HELLO WORLD
hello world
```

## Găsirea unui Caracter într-un Șir de Caractere în Java

Metoda `indexOf()` returnează indexul (poziția) primei apariții a unui text specificat într-un șir de caractere (inclusiv spațiile albe):

```java
String txt = "Please locate where 'locate' occurs!";
System.out.println(txt.indexOf("locate"));

output:
7
```




