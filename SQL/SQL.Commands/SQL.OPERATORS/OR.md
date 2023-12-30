# OR SQL

## Operatorul SQL OR
Clausula `WHERE` poate conține unul sau mai mulți operatori `OR`.

Operatorul OR este folosit pentru a filtra înregistrările pe baza a mai mult de o condiție, de exemplu, dacă dorești să returnezi toți clienții din Germania, dar și pe cei din Spania:


```sql
SELECT *
FROM Customers
WHERE Country = 'Germany' OR Country = 'Spain';
```

## Sintaxa

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...;
```

## OR vs AND
Operatorul `OR` afișează o înregistrare dacă oricare dintre condiții este ADEVĂRATĂ.

Operatorul `AND` afișează o înregistrare dacă toate condițiile sunt ADEVĂRATE.


| `CustomerID` | `CustomerName`                   | `ContactName`       | `Address`                    | `City`          | `PostalCode` | `Country` |
|------------|--------------------------------|-------------------|----------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders      | Obere Str. 57               | Berlin        | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno    | Mataderos 2312              | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.            | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8            | Luleå         | S-958 22   | Sweden  |


## Cel Puțin O Condiție Trebuie Să Fie Adevărată
Următoarea instrucțiune SQL selectează toate câmpurile din tabela `Customers` în care fie `City` este "Berlin", `CustomerName` începe cu litera "G" sau `Country` este "Norway":


```sql
SELECT * FROM Customers
WHERE City = 'Berlin' OR CustomerName LIKE 'G%' OR Country = 'Norway';
```

## Combinarea Operatorilor AND și OR
Poți combina operatorii `AND` și `OR`.

Următoarea instrucțiune SQL selectează toți clienții din Spania care încep cu "`G`" sau "`R`".

Asigură-te că folosești paranteze pentru a obține rezultatul corect.

```sql
SELECT * FROM Customers
WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%');
```
Fără paranteze, instrucțiunea `SELECT` va returna toți clienții din Spania care încep cu "`G`", plus toți clienții care încep cu "`R`", indiferent de valoarea țării:


Selectează toți clienții care fie:
- sunt din Spania și încep cu "G", sau
- încep cu litera "R":

```sql
SELECT * FROM Customers
WHERE Country = 'Spain' AND CustomerName LIKE 'G%' OR CustomerName LIKE 'R%';
```




