# Operatorii in SQL

## Operatori SQL

### Operatori Aritmetici

| `Operator` | `Descriere` | `Exemplu` |
|----------|-----------|---------|
| +        | Adunare   | 5 + 3   |
| -        | Scădere   | 8 - 2   |
| *        | Înmulțire | 4 * 6   |
| /        | Împărțire | 10 / 2  |
| %        | Modulo    | 7 % 3   |

### Operatori Biționali

| `Operator` | `Descriere`            |
|----------|----------------------|
| &        | Bițional ȘI          |
| \|       | Bițional SAU         |
| ^        | Bițional XOR         |

### Operatori de Comparare

| `Operator` | `Descriere`                           | `Exemplu`          |
|----------|-------------------------------------|------------------|
| =        | Egalitate                           | 5 = 5            |
| >        | Mai mare decât                      | 8 > 3            |
| <        | Mai mic decât                       | 4 < 7            |
| >=       | Mai mare sau egal decât             | 10 >= 10         |
| <=       | Mai mic sau egal decât              | 3 <= 6           |
| <>       | Diferit de                          | 7 <> 9           |

### Operatori Compunși

| `Operator` | `Descriere`             |
|----------|-----------------------|
| +=       | Adunare și atribuire |
| -=       | Scădere și atribuire |
| *=       | Înmulțire și atribuire|
| /=       | Împărțire și atribuire|
| %=       | Modulo și atribuire  |
| &=       | Bițional ȘI și atribuire |
| ^=       | Bițional XOR și atribuire|
| \|*=     | Bițional SAU și atribuire|

### Operatori Logici

| `Operator` | `Descriere`                                       | `Exemplu`               |
|----------|-----------------------------------------------|-----------------------|
| ALL      | Adevărat dacă toate valorile subquery îndeplinesc condiția | ALL (SELECT * FROM table) WHERE condition |
| AND      | Adevărat dacă toate condițiile separate de AND sunt adevărate | condition1 AND condition2 |
| ANY      | Adevărat dacă oricare dintre valorile subquery îndeplinesc condiția | ANY (SELECT * FROM table) WHERE condition |
| BETWEEN  | Adevărat dacă operandul se află în intervalul de comparații | value BETWEEN 10 AND 20 |
| EXISTS   | Adevărat dacă subquery returnează una sau mai multe înregistrări | EXISTS (SELECT * FROM table WHERE condition) |
| IN       | Adevărat dacă operandul este egal cu una din expresiile din listă | value IN (1, 2, 3) |
| LIKE     | Adevărat dacă operandul se potrivește cu un model specificat | text LIKE 'a%' |
| NOT      | Afișează înregistrarea dacă condiția nu este Adevărată | NOT condition        |
| OR       | Adevărat dacă oricare dintre condițiile separate de OR este adevărată | condition1 OR condition2 |
| SOME     | Adevărat dacă oricare dintre valorile subquery îndeplinesc condiția | SOME (SELECT * FROM table) WHERE condition |
