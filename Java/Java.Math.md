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


# Metodele Math

| Metodă            | Descriere                                                                                                      | Tipul Rezultatului        |
|-------------------|----------------------------------------------------------------------------------------------------------------|---------------------------|
| abs(x)            | Returnează valoarea absolută a lui x                                                                         | double|float|int|long      |
| acos(x)           | Returnează arccosinusul lui x, în radiani                                                                     | double                    |
| asin(x)           | Returnează arcsinusul lui x, în radiani                                                                      | double                    |
| atan(x)           | Returnează arcotangentul lui x ca o valoare numerică între -PI/2 și PI/2 radiani                             | double                    |
| atan2(y, x)       | Returnează unghiul theta din conversia coordonatelor rectangulare (x, y) în coordonate polare (r, theta)      | double                    |
| cbrt(x)           | Returnează rădăcina cubă a lui x                                                                             | double                    |
| ceil(x)           | Returnează valoarea lui x rotunjită în sus la cel mai apropiat număr întreg                                  | double                    |
| copySign(x, y)    | Returnează primul punct zecimal x cu semnul celui de-al doilea punct zecimal y                               | double                    |
| cos(x)            | Returnează cosinusul lui x (x este în radiani)                                                               | double                    |
| cosh(x)           | Returnează cosinusul hiperbolic al unei valori duble                                                           | double                    |
| exp(x)            | Returnează valoarea lui E la puterea x                                                                       | double                    |
| expm1(x)          | Returnează ex - 1                                                                                            | double                    |
| floor(x)          | Returnează valoarea lui x rotunjită în jos la cel mai apropiat număr întreg                                  | double                    |
| getExponent(x)    | Returnează exponentul neprelucrat utilizat în x                                                               | int                       |
| hypot(x, y)       | Returnează sqrt(x^2 + y^2) fără depășire sau subdepășire intermediară                                       | double                    |
| IEEEremainder(x, y)| Calculează operația de rest asupra lui x și y conform standardului IEEE 754                                 | double                    |
| log(x)            | Returnează logaritmul natural (bază E) al lui x                                                              | double                    |
| log10(x)          | Returnează logaritmul în baza 10 al lui x                                                                    | double                    |
| log1p(x)          | Returnează logaritmul natural (bază E) al sumei dintre x și 1                                              | double                    |
| max(x, y)         | Returnează numărul cu valoarea cea mai mare                                                                  | double|float|int|long      |
| min(x, y)         | Returnează numărul cu valoarea cea mai mică                                                                  | double|float|int|long      |
| nextAfter(x, y)   | Returnează numărul în virgulă mobilă adiacent lui x în direcția lui y                                       | double|float              |
| nextUp(x)         | Returnează valoarea în virgulă mobilă adiacentă lui x în direcția infinitului pozitiv                      | double|float              |
| pow(x, y)         | Returnează valoarea lui x la puterea lui y                                                                   | double                    |
| random()          | Returnează un număr aleatoriu între 0 și 1                                                                  | double                    |
| round(x)          | Returnează valoarea lui x rotunjită la cel mai apropiat număr întreg                                       | int                       |
| rint(x)           | Returnează valoarea dublă cea mai apropiată de x și egală cu un număr întreg matematic                       | double                    |
| signum(x)         | Returnează semnul lui x                                                                                     | double                    |
| sin(x)            | Returnează sinusul lui x (x este în radiani)                                                                | double                    |
| sinh(x)           | Returnează sinusul hiperbolic al unei valori duble                                                           | double                    |
| sqrt(x)           | Returnează rădăcina pătrată a lui x                                                                         | double                    |
| tan(x)            | Returnează tangenta unui unghi                                                                              | double                    |
| tanh(x)           | Returnează tangenta hiperbolică a unei valori duble                                                          | double                    |
| toDegrees(x)      | Convertește un unghi măsurat în radiani într-un unghi aproximativ echivalent măsurat în grade            | double                    |
| toRadians(x)      | Convertește un unghi măsurat în grade într-un unghi aproximativ măsurat în radiani                         | double                    |
| ulp(x)            | Returnează dimensiunea unității celei mai mici precizii (ulp) a lui x                                      | double|float              |

