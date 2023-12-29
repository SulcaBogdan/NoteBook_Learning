# Clasa Math in Java

Clasa Java Math are multe metode care îți permit să efectuezi operații matematice pe numere.

### Math.max(x,y)

Metoda `Math.max(x, y)` poate fi folosită pentru a găsi valoarea cea mai mare dintre `x` și `y`:

```java
Math.max(5,10);

output:
10
```

### Math.min(x,y)

Metoda `Math.min(x, y)` poate fi folosită pentru a găsi valoarea cea mai mică dintre `x` și `y`:

```java
Math.min(5, 10);

output:
5
```
### Math.sqrt(x)

Metoda `Math.sqrt(x)` returnează rădăcina pătrată a lui `x`:

```java
Math.sqrt(64);

output:
8.0
```

### Math.abd(x)

Metoda `Math.abs(x)` returnează valoarea absolută (pozitivă) a lui `x`:

```java
Math.abs(-4.7);

output:
4.7
```

## Random Numbers

Metoda `Math.random()` returnează un număr aleatoriu între 0.0 (inclusiv) și 1.0 (exclusiv):

```java
Math.random()

output:
0.11438035487934983
```
Pentru a obține mai mult control asupra numărului aleatoriu, de exemplu, dacă vrei doar un număr aleatoriu între 0 și 100, poți folosi formula următoare:
```java
int randomInRange = (int) (Math.random() * 101); // Generates a random number between 0 and 100
System.out.println(randomInRange);

output:
86
```



