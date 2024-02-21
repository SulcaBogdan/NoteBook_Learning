# Operatorii in Scala

Un `operator` este un simbol care îi spune compilatorului să efectueze anumite manipulări `matematice` sau `logice`. Scala este bogat în operatori încorporați și oferă următoarele tipuri de operatori −

- Operatori aritmetici
- Operatori Relaționali
- Operatori logici
- Operatori pe biți
- Operatori de atribuire

Acest capitol va examina operatorii `aritmetici`, `relaționali`, `logici`, pe `biți`, de `atribuire` și alți operatori unul câte unul.

## Operatori aritmetici
Următorii operatori aritmetici sunt acceptați de limbajul Scala. De exemplu, să presupunem că variabila A are 10 și variabila B 20, apoi −

| Operator | Descriere                                 | Exemplu                     |
|----------|-------------------------------------------|-----------------------------|
| `+`        | Adună cei doi operanzi                    | A + B va da 30              |
| `-`        | Scade al doilea operand din primul       | A - B va da -10            |
| `*`        | Înmulțește ambii operanzi                 | A * B va da 200            |
| `/`        | Împarte numărătorul la numitor            | B / A va da 2              |
| `%`        | Operatorul de modulo găsește restul împărțirii unui număr la altul | B % A va da 0            |


```scala
object Demo {
   def main(args: Array[String]) {
      var a = 10;
      var b = 20;
      
      println("a == b = " + (a == b) );
      println("a != b = " + (a != b) );
      println("a > b = " + (a > b) );
      println("a < b = " + (a < b) );
      println("b >= a = " + (b >= a) );
      println("b <= a = " + (b <= a) );
   }
}

output:
a == b = false
a != b = true
a > b = false
a < b = true
b >= a = true
b <= a = false
```

## Operatori logici
Următorii operatori logici sunt acceptați de limbajul Scala. De exemplu, să presupunem că variabila A deține 1 și variabila B deține 0, apoi -

```scala
object Demo {
   def main(args: Array[String]) {
      var a = true;
      var b = false;

      println("a && b = " + (a&&b) );
      
      println("a || b = " + (a||b) );
      
      println("!(a && b) = " + !(a && b) );
   }
} 

output:
a && b = false
a || b = true
!(a && b) = true
```

| Operator | Descriere                                                                          | Exemplu                 |
|----------|------------------------------------------------------------------------------------|-------------------------|
| `&&`       | Este numit operatorul logic ȘI (AND). Dacă ambii operanzi sunt nenuli, condiția devine adevărată. | (A && B) este fals.     |
| `\|\|`     | Este numit operatorul logic SAU (OR). Dacă oricare dintre cei doi operanzi este nenul, condiția devine adevărată. | (A \|\| B) este adevărat. |
| `!`        | Este numit operatorul logic NU (NOT). Este folosit pentru a inversa starea logică a operandului său. Dacă o condiție este adevărată, atunci operatorul logic NU o va face falsă. | !(A && B) este adevărat. |

## Operatori pe biți
Operatorul pe biți lucrează pe biți și efectuează operațiuni bit cu bit. Tabelele de adevăr pentru &, | și ^ sunt după cum urmează -

| p | q | p & q | p \| q | p ^ q |
|---|---|-------|--------|-------|
| 0 | 0 | 0     | 0      | 0     |
| 0 | 1 | 0     | 1      | 1     |
| 1 | 1 | 1     | 1      | 0     |
| 1 | 0 | 0     | 1      | 1     |


Să presupunem că A = 60; şi B = 13; acum în format binar vor fi după cum urmează −

```
A = 0011 1100
B = 0000 1101
-----------------------
A&B = 0000 1100
A|B = 0011 1101
A^B = 0011 0001
~A = 1100 0011
```

Operatorii pe biți acceptați de limbajul Scala sunt enumerați în tabelul următor. Să presupunem că variabila A deține 60 și variabila B deține 13, apoi −

```scala
object Demo {
   def main(args: Array[String]) {
      var a = 60;           /* 60 = 0011 1100 */  
      var b = 13;           /* 13 = 0000 1101 */
      var c = 0;

      c = a & b;            /* 12 = 0000 1100 */ 
      println("a & b = " + c );

      c = a | b;            /* 61 = 0011 1101 */
      println("a | b = " + c );

      c = a ^ b;            /* 49 = 0011 0001 */
      println("a ^ b = " + c );

      c = ~a;               /* -61 = 1100 0011 */
      println("~a = " + c );

      c = a << 2;           /* 240 = 1111 0000 */
      println("a << 2 = " + c );

      c = a >> 2;           /* 215 = 1111 */
      println("a >> 2  = " + c );

      c = a >>> 2;          /* 215 = 0000 1111 */
      println("a >>> 2 = " + c );
   }
} 
```

| Operator | Descriere                                                                                       | Exemplu                          |
|----------|-------------------------------------------------------------------------------------------------|----------------------------------|
| `&`        | Operatorul binar ȘI (AND) copiază un bit în rezultat dacă există în ambii operanzi.             | (A & B) va da 12, care este 0000 1100 |
| `\|`       | Operatorul binar SAU (OR) copiază un bit dacă există în oricare dintre operanzi.                | (A \| B) va da 61, care este 0011 1101 |
| `^`        | Operatorul binar XOR copiază bitul dacă este setat într-un operand dar nu în amândoi.           | (A ^ B) va da 49, care este 0011 0001 |
| `~`        | Operatorul de complement unar binar 'inversează' biții.                                        | (~A) va da -61, care este 1100 0011 în forma complementului de 2 datorită unui număr binar semnat. |
| `<<`       | Operatorul de deplasare binară la stânga. Pozițiile bitului valorii operandului stâng sunt mutate la stânga cu numărul de biți specificat de operandul drept. | A << 2 va da 240, care este 1111 0000 |
| `>>`       | Operatorul de deplasare binară la dreapta. Pozițiile bitului valorii operandului stâng sunt mutate la dreapta cu numărul de biți specificat de operandul drept. | A >> 2 va da 15, care este 1111 |
| `>>>`      | Operatorul de deplasare la dreapta cu umplere cu zero. Valoarea operandului stâng este mutată la dreapta cu numărul de biți specificat de operandul drept și valorile deplasate sunt umplute cu zerouri. | A >>> 2 va da 15 care este 0000 1111 |


## Operatori de atribuire
Există următorii operatori de atribuire acceptați de limbajul Scala −

| Operator | Descriere                                                                                       | Exemplu                                   |
|----------|-------------------------------------------------------------------------------------------------|-------------------------------------------|
| `=`        | Operatorul simplu de atribuire, atribuie valorile de la operandele din dreapta la operandele din stânga. | C = A + B va atribui valoarea A + B lui C |
| `+=`       | Operatorul de atribuire cu adunare, adaugă operandul din dreapta la operandul din stânga și atribuie rezultatul la operandul din stânga. | C += A este echivalent cu C = C + A         |
| `-=`       | Operatorul de atribuire cu scădere, scade operandul din dreapta din operandul din stânga și atribuie rezultatul la operandul din stânga. | C -= A este echivalent cu C = C - A         |
|`*=`       | Operatorul de atribuire cu înmulțire, înmulțește operandul din stânga cu operandul din dreapta și atribuie rezultatul la operandul din stânga. | C *= A este echivalent cu C = C * A         |
| `/=`       | Operatorul de atribuire cu împărțire, împarte operandul din stânga la operandul din dreapta și atribuie rezultatul la operandul din stânga. | C /= A este echivalent cu C = C / A         |
| `%=`       | Operatorul de atribuire cu rest, calculează restul împărțirii operandului din stânga la operandul din dreapta și atribuie rezultatul la operandul din stânga. | C %= A este echivalent cu C = C % A         |
| `<<=`      | Operatorul de atribuire cu deplasare la stânga, deplasează la stânga operandul din stânga cu numărul specificat de biți și atribuie rezultatul la operandul din stânga. | C <<= 2 este la fel ca și C = C << 2        |
| `>>=`      | Operatorul de atribuire cu deplasare la dreapta, deplasează la dreapta operandul din stânga cu numărul specificat de biți și atribuie rezultatul la operandul din stânga. | C >>= 2 este la fel ca și C = C >> 2        |
| `&=`       | Operatorul de atribuire cu ȘI pe biți, efectuează operația de ȘI pe biți între operandul din stânga și operandul din dreapta și atribuie rezultatul la operandul din stânga. | C &= 2 este la fel ca și C = C & 2          |
| `^=`       | Operatorul de atribuire cu XOR pe biți, efectuează operația de XOR pe biți între operandul din stânga și operandul din dreapta și atribuie rezultatul la operandul din stânga. | C ^= 2 este la fel ca și C = C ^ 2          |
| `\|=`      | Operatorul de atribuire cu SAU pe biți, efectuează operația de SAU pe biți între operandul din stânga și operandul din dreapta și atribuie rezultatul la operandul din stânga. | C \|= 2 este la fel ca și C = C \| 2        |


```scala
object Demo {
   def main(args: Array[String]) {
      var a = 10;	
      var b = 20;
      var c = 0;

      c = a + b;
      println("c = a + b  = " + c );

      c += a ;
      println("c += a  = " + c );

      c -= a ;
      println("c -= a = " + c );

      c *= a ;
      println("c *= a = " + c );

      a = 10;
      c = 15;
      c /= a ;
      println("c /= a  = " + c );

      a = 10;
      c = 15;
      c %= a ;
      println("c %= a  = " + c );

      c <<= 2 ;
      println("c <<= 2  = " + c );

      c >>= 2 ;
      println("c >>= 2  = " + c );

      c >>= 2 ;
      println("c >>= 2  = " + c );

      c &= a ;
      println("c &= a  = " + c );
     
      c ^= a ;
      println("c ^= a  = " + c );

      c |= a ;
      println("c |= a  = " + c );
   }
} 

Output:
c = a + b  = 30
c += a  = 40
c -= a  = 30
c *= a  = 300
c /= a  = 1
c %= a  = 5
c <<= 2  = 20
c >>= 2  = 5
c >>= 2  = 1
c &= a  = 0
c ^= a  = 10
c |= a  = 10
```

## Precedenta operatorilor la Scala
Prioritatea operatorului determină gruparea termenilor într-o expresie. Acest lucru afectează modul în care o expresie este evaluată. Unii operatori au prioritate mai mare decât alții; de exemplu, operatorul de înmulțire are o prioritate mai mare decât operatorul de adunare −

De exemplu, `x = 7 + 3 * 2;` aici, lui x i se atribuie 13, nu 20, deoarece operatorul * are o prioritate mai mare decât +, așa că mai întâi se înmulțește cu 3*2 și apoi se adună în 7.

Aruncă o privire la următorul tabel. Operatorii cu cea mai mare prioritate apar în partea de sus a tabelului, iar cei cu cea mai mică prioritate apar în partea de jos. În cadrul unei expresii, operatorii cu prioritate mai mare vor fi evaluați mai întâi.

| Categorie     | Operator                   | Asociativitate    |
|---------------|----------------------------|-------------------|
| Postfix       | () []                      | Stânga la dreapta |
| Unary         | ! ~                        | Dreapta la stânga |
| Multiplicative| * / %                      | Stânga la dreapta |
| Additive      | + -                        | Stânga la dreapta |
| Shift         | >> >>> <<                  | Stânga la dreapta |
| Relational    | > >= < <=                  | Stânga la dreapta |
| Equality      | == !=                      | Stânga la dreapta |
| Bitwise AND   | &                          | Stânga la dreapta |
| Bitwise XOR   | ^                          | Stânga la dreapta |
| Bitwise OR    | \|                         | Stânga la dreapta |
| Logical AND   | &&                         | Stânga la dreapta |
| Logical OR    | \|\|                       | Stânga la dreapta |
| Assignment    | = += -= *= /= %= >>= <<= &= ^= \|= | Dreapta la stânga |
| Comma         | ,                          | Stânga la dreapta |
