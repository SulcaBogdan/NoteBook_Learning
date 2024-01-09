# EXISTS in SQL

Operatorul `EXISTS` este folosit pentru a testa existența oricărei înregistrări într-o **subinterogare**.

Operatorul `EXISTS` returnează `TRUE` dacă subinterogarea returnează una sau mai multe înregistrări.

## Sintaxa EXISTĂ 

```sql
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);
```

Mai jos este o selecție din tabelul `Products` din baza de date exemplu `Northwind`:

| `ProductID` | `ProductName`                   | `SupplierID` | `CategoryID` | `Unit`                 | `Price` |
|-----------|-------------------------------|------------|------------|----------------------|-------|
| 1         | Chais                         | 1          | 1          | 10 boxes x 20 bags   | 18    |
| 2         | Chang                         | 1          | 1          | 24 - 12 oz bottles  | 19    |
| 3         | Aniseed Syrup                 | 1          | 2          | 12 - 550 ml bottles | 10    |
| 4         | Chef Anton's Cajun Seasoning  | 2          | 2          | 48 - 6 oz jars       | 22    |
| 5         | Chef Anton's Gumbo Mix        | 2          | 2          | 36 boxes             | 21.35 |

Și o selecție din tabelul `Suppliers`:

| `SupplierID` | `SupplierName`                    | `ContactName`    | `Address`                     | `City`           | `PostalCode` | `Country` |
|------------|---------------------------------|-----------------|-----------------------------|----------------|------------|---------|
| 1          | Exotic Liquid                   | Charlotte Cooper | 49 Gilbert St.              | London         | EC1 4SD    | UK      |
| 2          | New Orleans Cajun Delights      | Shelley Burke    | P.O. Box 78934              | New Orleans    | 70117      | USA     |
| 3          | Grandma Kelly's Homestead       | Regina Murphy    | 707 Oxford Rd.              | Ann Arbor      | 48104      | USA     |
| 4          | Tokyo Traders                   | Yoshi Nagase     | 9-8 Sekimai Musashino-shi   | Tokyo          | 100        | Japan   |


## Exemple SQL EXISTS 
Următoarea instrucțiune SQL returnează `TRUE` și listează furnizorii cu un preț al produsului mai mic de 20:

```SQL
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);
```

Următoarea instrucțiune SQL returnează `TRUE` și listează furnizorii cu un preț al produsului egal cu 22:

```SQL
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price = 22);
```

