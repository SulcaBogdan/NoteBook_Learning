# NOT SQL

## Operatorul NOT
Operatorul `NOT` este folosit în combinație cu alți operatori pentru a obține rezultatul opus, cunoscut și sub denumirea de rezultat negativ.

În instrucțiunea `SELECT` de mai jos, dorim să returnăm toți clienții care NU sunt din Spania:


```sql
SELECT * FROM Customers
WHERE NOT Country = 'Spain';
```

În exemplul de mai sus, operatorul `NOT` este folosit în combinație cu operatorul `=`, dar poate fi folosit în combinație cu alți operatori de comparație și/sau logici. Vezi exemplele de mai jos.

## Sintaxa

```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```
| CustomerID | CustomerName                   | ContactName       | Address                    | City          | PostalCode | Country |
|------------|--------------------------------|-------------------|----------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders      | Obere Str. 57               | Berlin        | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno    | Mataderos 2312              | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.            | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8            | Luleå         | S-958 22   | Sweden  |


## NOT LIKE
```sql
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'A%';
```

## NOT BETWEEN

```sql
SELECT * FROM Customers
WHERE CustomerID NOT BETWEEN 10 AND 60;
```

## NOT IN

```sql
SELECT * FROM Customers
WHERE City NOT IN ('Paris', 'London');
```

## NOT Greater Than

```sql
SELECT * FROM Customers
WHERE NOT CustomerID > 50;
```
Notă: Există un operator not-mai-mare-decât: `!>` care îți va oferi același rezultat.

## NOT Less Than


```sql
SELECT * FROM Customers
WHERE NOT CustomerId < 50;
```

Notă: Există un operator not-mai-mic-decât: `!<` care îți va oferi același rezultat.

