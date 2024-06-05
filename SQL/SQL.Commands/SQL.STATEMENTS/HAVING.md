# HAVING in SQL

Clauza `HAVING` a fost adăugată la SQL deoarece cuvântul cheie `WHERE` nu poate fi utilizat cu **funcții de agregare**.

## Sintaxă HABVING 

```SQL
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);
```

Mai jos este o selecție din tabelul `Clients` din baza de date exemplu `Northwind`:


| `CustomerID` | `CustomerName`                      | `ContactName`      | `Address`                   | `City`           | `PostalCode` | `Country` |
|------------|----------------------------------|-------------------|---------------------------|----------------|------------|---------|
| 1          | Alfreds Futterkiste              | Maria Anders      | Obere Str. 57             | Berlin         | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados| Ana Trujillo     | Avda. de la Constitución 2222 | México D.F.  | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería          | Antonio Moreno    | Mataderos 2312            | México D.F.    | 05023      | Mexico  |
| 4          | Around the Horn                   | Thomas Hardy      | 120 Hanover Sq.           | London         | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp                | Christina Berglund| Berguvsvägen 8            | Luleå          | S-958 22   | Sweden  |


## Exemplu SQL HAVING 
Următoarea instrucțiune SQL listează numărul de clienți din fiecare țară. Includeți numai țările cu mai mult de 5 clienți:

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```

Următoarea instrucțiune SQL listează numărul de clienți din fiecare țară, sortați de la sus la cel mai mic (includeți numai țările cu mai mult de 5 clienți):

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

Mai jos este o selecție din tabelul `Orders` din baza de date exemplu `Northwind`:

| `OrderID` | `CustomerID` | `EmployeeID` | `OrderDate`  | `ShipperID` |
|---------|------------|------------|------------|-----------|
| 10248   | 90         | 5          | 1996-07-04 | 3         |
| 10249   | 81         | 6          | 1996-07-05 | 1         |
| 10250   | 34         | 4          | 1996-07-08 | 2         |

Și o selecție din tabelul `Employees`:

| `EmployeeID` | `LastName`  | `FirstName` | `BirthDate`  | `Photo`      | `Notes`                            |
|------------|-----------|-----------|------------|------------|----------------------------------|
| 1          | Davolio   | Nancy     | 1968-12-08 | EmpID1.pic | Education includes a BA....      |
| 2          | Fuller    | Andrew    | 1952-02-19 | EmpID2.pic | Andrew received his BTS....      |
| 3          | Leverling | Janet     | 1963-08-30 | EmpID3.pic | Janet has a BS degree....        |


## Mai multe Exemple HAVING 
Următoarea instrucțiune SQL listează angajații care au înregistrat mai mult de 10 comenzi:

```sql
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM (Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID)
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 10;
```

Următoarea instrucțiune SQL listează dacă angajații `„Davolio”` sau `„Fuller”` au înregistrat mai mult de 25 de comenzi:

```sql
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
WHERE LastName = 'Davolio' OR LastName = 'Fuller'
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 25;
```

