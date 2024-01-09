# SQL FULL OUTER JOIN

Cuvântul cheie `FULL OUTER JOIN` returnează toate înregistrările atunci când există o potrivire în înregistrările tabelului din stânga (tabelul 1) sau din dreapta (tabelul 2).

`Nota`: `FULL OUTER JOIN `și `FULL JOIN` sunt aceleași.

## Sintaxă FULL OUTER JOIN

```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name
WHERE condition;
```

`Notă`: `FULL OUTER JOIN` poate returna seturi de rezultate foarte mari!


În acest tutorial vom folosi binecunoscuta bază de date mostre `Northwind`.

Mai jos este o selecție din tabelul `Clients`:

| `CustomerID` | `CustomerName`                      | `ContactName`    | `Address`                          | `City`           | `PostalCode` | `Country` |
|------------|----------------------------------|-----------------|----------------------------------|----------------|------------|---------|
| 1          | Alfreds Futterkiste              | Maria Anders    | Obere Str. 57                    | Berlin         | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados| Ana Trujillo    | Avda. de la Constitución 2222    | México D.F.    | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería          | Antonio Moreno  | Mataderos 2312                   | México D.F.    | 05023      | Mexico  |


Și o selecție din tabelul `Orders`:

| `OrderID` | `CustomerID` | `EmployeeID` | `OrderDate`  | `ShipperID` |
|---------|------------|------------|------------|-----------|
| 10308   | 2          | 7          | 1996-09-18 | 3         |
| 10309   | 37         | 3          | 1996-09-19 | 1         |
| 10310   | 77         | 8          | 1996-09-20 | 2         |


## Exemplu SQL FULL OUTER JOIN
Următoarea instrucțiune SQL selectează toți clienții și toate comenzile:

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;
```

O selecție din setul de rezultate poate arăta astfel:

| `CustomerName`                       | `OrderID` |
|------------------------------------|---------|
| Null                               | 10309   |
| Null                               | 10310   |
| Alfreds Futterkiste                | Null    |
| Ana Trujillo Emparedados y helados | 10308   |
| Antonio Moreno Taquería            | Null    |

`Notă`: cuvântul cheie `FULL OUTER JOIN` returnează toate înregistrările care se potrivesc din ambele tabele, indiferent dacă celălalt tabel se potrivește sau nu. Deci, dacă există rânduri în `Clients` care nu au potriviri în `Orders`, sau dacă există rânduri în `Clients` care nu au potriviri în `Clients`, vor fi listate și acele rânduri.


