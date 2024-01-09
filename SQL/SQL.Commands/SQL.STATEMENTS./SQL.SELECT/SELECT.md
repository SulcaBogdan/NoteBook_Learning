# SQL SELECT

Instrucțiunea `SELECT` este folosită pentru a selecta date dintr-o bază de date.

```sql
SELECT CustomerName, City 
FROM Customers;
```

# Sintaxa

```sql
SELECT column1, column2, ...
FROM table_name;
```

| `CustomerID` | `CustomerName`                   | `ContactName`       | `Address`                    | `City`          | `PostalCode` | `Country` |
|------------|--------------------------------|-------------------|----------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders      | Obere Str. 57               | Berlin        | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno    | Mataderos 2312              | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.            | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8            | Luleå         | S-958 22   | Sweden  |


## Selectează TOATE Coloanele 
Dacă dorești să returnezi toate coloanele, fără a specifica fiecare nume de coloană, poți folosi sintaxa `SELECT *`:

```sql
SELECT * 
FROM Customers;
```




