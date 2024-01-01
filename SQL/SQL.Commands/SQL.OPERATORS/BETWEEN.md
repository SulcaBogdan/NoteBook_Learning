# BETWEEN SQL

## Operatorul SQL BETWEEN
Operatorul `BETWEEN` selectează valorile dintr-un interval dat. Valorile pot fi numere, texte sau date.

Operatorul `BETWEEN` este inclusiv: valorile de început și de sfârșit sunt incluse.

### Exemplu
Selectează toate produsele cu un preț cuprins între 10 și 20:

## Sintaxa

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

| ProductID | ProductName                  | SupplierID | CategoryID | Unit                  | Price |
|-----------|------------------------------|------------|------------|-----------------------|-------|
| 1         | Chais                        | 1          | 1          | 10 cutii x 20 pungi   | 18    |
| 2         | Chang                        | 1          | 1          | 24 sticle de 12 oz    | 19    |
| 3         | Aniseed Syrup                | 1          | 2          | 12 sticle de 550 ml   | 10    |
| 4         | Chef Anton's Cajun Seasoning | 2          | 2          | 48 sticle de 6 oz     | 22    |
| 5         | Chef Anton's Gumbo Mix       | 2          | 2          | 36 cutii              | 21.35 |


## NOT BETWEEN
Pentru a afișa produsele în afara intervalului din exemplul anterior, folosește `NOT BETWEEN`:

Exemplu
```sql
SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;
```

## BETWEEN cu IN
Următorul declarație SQL selectează toate produsele cu un preț între 10 și 20. În plus, `CategoryID` trebuie să fie fie 1, 2 sau 3:

```sql
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20
AND CategoryID IN (1,2,3);
```
## BETWEEN cu valori text
Următoarea declarație SQL selectează toate produsele cu un nume de produs în ordine alfabetică între 'Carnarvon Tigers' și 'Mozzarella di Giovanni':

```sql
SELECT * FROM Products
WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY ProductName;
```

Următoarea declarație SQL selectează toate produsele cu un nume de produs între 'Carnarvon Tigers' și 'Chef Anton's Cajun Seasoning':


## NOT BETWEEN cu valori text
Următoarea declarație SQL selectează toate produsele cu un nume de produs în afara intervalului dintre 'Carnarvon Tigers' și 'Mozzarella di Giovanni':

```sql
SELECT * FROM Products
WHERE ProductName NOT BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY ProductName;
```
## BETWEEN cu date
Următoarea declarație SQL selectează toate comenzile cu o dată de comandă între '01-Iulie-1996' și '31-Iulie-1996':

```sql
SELECT * FROM Orders
WHERE OrderDate BETWEEN #07/01/1996# AND #07/31/1996#;
```

SAU

```sql
SELECT * FROM Orders
WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';
```


| OrderID | CustomerID | EmployeeID | OrderDate    | ShipperID |
|---------|------------|------------|--------------|-----------|
| 10248   | 90         | 5          | 4-Iulie-1996 | 3         |
| 10249   | 81         | 6          | 5-Iulie-1996 | 1         |
| 10250   | 34         | 4          | 8-Iulie-1996 | 2         |
| 10251   | 84         | 3          | 9-Iulie-1996 | 1         |
| 10252   | 76         | 4          | 10-Iulie-1996| 2         |


