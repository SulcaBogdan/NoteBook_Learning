# Concatenarea in Java

## Concatenarea Șirurilor în Java

Operatorul `+` poate fi folosit între șiruri pentru a le combina. Aceasta se numește concatenare:

```java
String firstName = "John";
String lastName = "Doe";
System.out.println(firstName + " " + lastName);

output:
John Doe
```
**Notă** că am adăugat un text gol `(" ")` pentru a crea un spațiu între `firstName` și lastName la afișare.


Poți folosi, de asemenea, metoda `concat()` pentru a concatena două șiruri:

```java
String firstName = "John ";
String lastName = "Doe";
System.out.println(firstName.concat(lastName));

output:
John Doe
```

