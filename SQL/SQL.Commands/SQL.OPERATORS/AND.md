# AND SQL

## Operatorul SQL AND
Clausula `WHERE` poate conține unul sau mai mulți operatori `AND`.

Operatorul `AND` este folosit pentru a filtra înregistrările pe baza a mai mult de o condiție, de exemplu, dacă dorești să returnezi toți clienții din Spania care încep cu litera 'G':


```sql
SELECT *
FROM Customers
WHERE Country = 'Spain' AND CustomerName LIKE 'G%';
```

## Sintaxa

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```

## AND vs OR
Operatorul `AND` afișează o înregistrare dacă toate condițiile sunt ADEVĂRATE.

Operatorul `OR` afișează o înregistrare dacă oricare dintre condiții este ADEVĂRATĂ.


| CustomerID | CustomerName                   | ContactName       | Address                    | City          | PostalCode | Country |
|------------|--------------------------------|-------------------|----------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders      | Obere Str. 57               | Berlin        | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno    | Mataderos 2312              | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.            | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8            | Luleå         | S-958 22   | Sweden  |


## Toate Condițiile Trebuie să Fie Adevărate
Următoarea instrucțiune SQL selectează toate câmpurile din Customers în care țara este "Germany" ȘI orașul este "Berlin" ȘI codul poștal este mai mare de 12000:

```sql
SELECT * FROM Customers
WHERE Country = 'Germany'
AND City = 'Berlin'
AND PostalCode > '12000';
```
## Combinarea Operatorilor AND și OR
Poți combina operatorii `AND` și `OR`.

Următoarea instrucțiune SQL selectează toți clienții din Spania care încep cu "G" sau "R".

Asigură-te că folosești paranteze pentru a obține rezultatul corect.


```sql
SELECT * FROM Customers
WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%');
```

Fără paranteze, instrucțiunea `SELECT` va returna toți clienții din Spania care încep cu "G", plus toți clienții care încep cu "R", indiferent de valoarea țării:


Selectează toți clienții care fie:
- sunt din Spania și încep cu "G", sau
- încep cu litera "R":


```sql
SELECT * FROM Customers
WHERE Country = 'Spain' AND CustomerName LIKE 'G%' OR CustomerName LIKE 'R%';
```
