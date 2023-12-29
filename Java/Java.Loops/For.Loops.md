# For Loops in Java

## Bucla `for`

Când știi exact de câte ori vrei să parcurgi un bloc de cod, folosește bucla `for` în loc de bucla `while`:

```java
for (statement 1; statement 2; statement 3) {
  // blocul de cod
}
```

### Exemplu buclă `for`

- Statement 1 este executată (o singură dată) înainte de execuția blocului de cod.

- Statement 2 definește condiția pentru executarea blocului de cod.

- Statement 3 este executată (de fiecare dată) după ce blocul de cod a fost executat.

```java
for (int i = 0; i < 5; i++) {
  System.out.println(i);
}

output:
0
1
2
3
4
```

- Statement 1 setează o variabilă înainte ca bucla să înceapă (int i = 0).

- Statement 2 definește condiția pentru executarea buclei (i trebuie să fie mai mic decât 5). Dacă condiția este adevărată, bucla va începe din nou, iar dacă este falsă, bucla se va încheia.

- Statement 3 crește o valoare (i++) de fiecare dată când blocul de cod din buclă a fost executat.


Un alt exemplu

```java
for (int i = 0; i <= 10; i = i + 2) {
  System.out.println(i);
}

output:
0
2
4
6
8
10
```

### Nested loops

Este posibil să plasezi o buclă în interiorul altei bucle. Acest lucru se numește **nested loop**.

"Bucla interioară" va fi executată o dată pentru fiecare iterație a "buclei exterioare".

```java
// Outer loop
for (int i = 1; i <= 2; i++) {
  System.out.println("Outer: " + i); // Executes 2 times
  
  // Inner loop
  for (int j = 1; j <= 3; j++) {
    System.out.println(" Inner: " + j); // Executes 6 times (2 * 3)
  }
} 

output:
Outer: 1
 Inner: 1
 Inner: 2
 Inner: 3
Outer: 2
 Inner: 1
 Inner: 2
 Inner: 3
```


