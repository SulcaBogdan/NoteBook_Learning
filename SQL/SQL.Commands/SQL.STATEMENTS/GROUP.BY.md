# GROUP BY in SQL


Instrucțiunea `GROUP BY` grupează rândurile care au aceleași valori în rânduri rezumative, cum ar fi „găsiți numărul de clienți din fiecare țară”.

Instrucțiunea `GROUP BY `este adesea folosită cu funcții agregate (`COUNT()`, `MAX()`, `MIN()`, `SUM()`, `AVG()`) pentru a grupa setul de rezultate după una sau mai multe coloane.

## Sintaxa GROUP BY 


```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
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


## Exemplu SQL GROUP BY 
Următoarea instrucțiune SQL listează numărul de clienți din fiecare țară:

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;
```

Următoarea instrucțiune SQL listează numărul de clienți din fiecare țară, sortați de la sus la mai mic:

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
```

Mai jos este o selecție din tabelul `Orders` din baza de date exemplu `Northwind`:

| `OrderID` | `CustomerID` | `EmployeeID` | `OrderDate`  | `ShipperID` |
|---------|------------|------------|------------|-----------|
| 10248   | 90         | 5          | 1996-07-04 | 3         |
| 10249   | 81         | 6          | 1996-07-05 | 1         |
| 10250   | 34         | 4          | 1996-07-08 | 2         |


Și o selecție din tabelul `Shippers`:

| `ShipperID` | `ShipperName`      |
|-----------|------------------|
| 1         | Speedy Express   |
| 2         | United Package   |
| 3         | Federal Shipping |

## GROUP BY Cu JOIN Exemplu
Următoarea instrucțiune SQL listează numărul de comenzi trimise de fiecare expeditor:

```sql
SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders
LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;
```


