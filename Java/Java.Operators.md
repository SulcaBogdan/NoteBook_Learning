# Operatorii Java

## Operatori Java

Operatorii sunt folosiți pentru a efectua operații pe variabile și valori.

În exemplul de mai jos, folosim operatorul + pentru a aduna două valori:


```java
int x = 100 + 50;
```

Deși operatorul `+` este adesea folosit pentru a aduna două valori, așa cum este în exemplul de mai sus, poate fi folosit și pentru a aduna o variabilă și o valoare, sau o variabilă și alta variabilă:


```java
int sum1 = 100 + 50;        // 150 (100 + 50)
int sum2 = sum1 + 250;      // 400 (150 + 250)
int sum3 = sum2 + sum2;     // 800 (400 + 400)
```

Java împarte operatorii în următoarele grupuri:

- Operatori aritmetici
- Operatori de atribuire
- Operatori de comparație
- Operatori logici
- Operatori pe biți


## Operatori Aritmetici

Operatorii aritmetici sunt folosiți pentru a realiza operații matematice comune.

| Operator | Nume        | Descriere                                               | Exemplu  |
|----------|-------------|---------------------------------------------------------|----------|
| +        | Adunare     | Adună două valori                                      | x + y    |
| -        | Scădere     | Scade o valoare din alta                                | x - y    |
| *        | Înmulțire   | Înmulțește două valori                                  | x * y    |
| /        | Împărțire   | Împarte o valoare la alta                                | x / y    |
| %        | Modul       | Returnează restul împărțirii                            | x % y    |
| ++       | Incrementare | Crește valoarea unei variabile cu 1                     | ++x      |
| --       | Decrementare | Scade valoarea unei variabile cu 1                      | --x      |


## Operatori de Atribuire în Java

Operatorii de atribuire sunt folosiți pentru a atribui valori variabilelor.

În exemplul de mai jos, folosim operatorul de atribuire (=) pentru a atribui valoarea 10 unei variabile numite x:


```java
int x = 10;
```

Operatorul de atribuire adițională `(+=)` adaugă o valoare la o variabilă:

```java
int x = 10;
x += 5;
```

| Operator | Exemplu   | Echivalent cu      |
|----------|-----------|---------------------|
| =        | x = 5     | x = 5               |
| +=       | x += 3    | x = x + 3           |
| -=       | x -= 3    | x = x - 3           |
| *=       | x *= 3    | x = x * 3           |
| /=       | x /= 3    | x = x / 3           |
| %=       | x %= 3    | x = x % 3           |
| &=       | x &= 3    | x = x & 3           |
| |=       | x |= 3    | x = x | 3           |
| ^=       | x ^= 3    | x = x ^ 3           |
| >>=      | x >>= 3   | x = x >> 3          |
| <<=      | x <<= 3   | x = x << 3          |


## Operatori de Comparație în Java

Operatorii de comparație sunt folosiți pentru a compara două valori (sau variabile). Acest lucru este important în programare, deoarece ne ajută să găsim răspunsuri și să luăm decizii.

Valoarea returnată de o comparație este fie adevărată (true), fie falsă (false). Aceste valori sunt cunoscute sub numele de valori booleene, iar vei afla mai multe despre ele în capitolul Booleans și If..Else.

În exemplul următor, folosim operatorul mai mare decât (>) pentru a afla dacă 5 este mai mare decât 3:

```java
int x = 5;
int y = 3;
System.out.println(x > y);

output:
true
```

| Operator | Nume                  | Exemplu      |
|----------|-----------------------|--------------|
| ==       | Egal cu               | x == y       |
| !=       | Diferit de            | x != y       |
| >        | Mai mare decât        | x > y        |
| <        | Mai mic decât          | x < y        |
| >=       | Mai mare sau egal cu   | x >= y       |
| <=       | Mai mic sau egal cu    | x <= y       |


## Operatori Logici în Java

Poți testa, de asemenea, valori adevărate sau false cu ajutorul operatorilor logici.

Operatorii logici sunt folosiți pentru a determina logica între variabile sau valori:

| Operator | Nume         | Descriere                                    | Exemplu                |
|----------|--------------|----------------------------------------------|------------------------|
| &&       | Logica și    | Returnează true dacă ambele afirmații sunt adevărate | x < 5 && x < 10       |
| \|\|      | Logica sau   | Returnează true dacă una dintre afirmații este adevărată | x < 5 \|\| x < 4      |
| !        | Logica not   | Inversează rezultatul, returnează false dacă rezultatul este adevărat | !(x < 5 && x < 10)    |
