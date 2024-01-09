# RIGHT JOIN in SQL

## SQL RIGHT JOIN Keyword

Cuvântul cheie `RIGHT JOIN` returnează toate înregistrările din tabela dreaptă (table2) și înregistrările care se potrivesc din tabela stângă (table1). Rezultatul este de 0 înregistrări din partea stângă, dacă nu există nicio potrivire.

## Sintaxa RIGHT JOIN

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

În unele baze de date, `RIGHT JOIN` este denumit și `RIGHT OUTER JOIN`.


În acest tutorial, vom folosi cunoscuta bază de date demonstrativă `Northwind`.

Mai jos este o selecție din tabela "`Orders`":

| OrderID | CustomerID | EmployeeID | OrderDate  | ShipperID |
|---------|------------|------------|------------|-----------|
| 10308   | 2          | 7          | 1996-09-18 | 3         |
| 10309   | 37         | 3          | 1996-09-19 | 1         |
| 10310   | 77         | 8          | 1996-09-20 | 2         |


Și o selecție din tabela "`Employees`":

| EmployeeID | LastName  | FirstName | BirthDate  | Photo        |
|------------|-----------|-----------|------------|--------------|
| 1          | Davolio   | Nancy     | 12/8/1968  | EmpID1.pic   |
| 2          | Fuller    | Andrew    | 2/19/1952  | EmpID2.pic   |
| 3          | Leverling | Janet     | 8/30/1963  | EmpID3.pic   |


## Exemplu SQL RIGHT JOIN
Următoarea instrucțiune SQL va returna toți angajații și orice comenzi pe care le-ar fi putut plasa:

```sql
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;
```
`Notă`: cuvântul cheie `RIGHT JOIN` returnează toate înregistrările din tabelul din dreapta (`Employees`), chiar dacă nu există potriviri în tabelul din stânga (`Orders`).

