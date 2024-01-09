# INSERT INTO SELECT in SQL

Instrucțiunea `INSERT INTO SELECT` copiază datele dintr-un tabel și le inserează într-un alt tabel.

Instrucțiunea` INSERT INTO SELECT` necesită ca tipurile de date din tabelele sursă și țintă să se potrivească.

`Notă`: Înregistrările existente în tabelul țintă nu sunt afectate.

## Sintaxă INSERT INTO SELECT
Copiați toate coloanele dintr-un tabel în altul:

```sql
INSERT INTO table2
SELECT * FROM table1
WHERE condition;
```
Copiați doar câteva coloane dintr-un tabel în alt tabel:

```sql
INSERT INTO table2 (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;
```

În acest tutorial vom folosi binecunoscuta bază de date mostre Northwind.

Mai jos este o selecție din tabelul `Clients`:

| `CustomerID` | `CustomerName`                      | `ContactName`      | `Address`                   | `City`           | `PostalCode` | `Country` |
|------------|----------------------------------|-------------------|---------------------------|----------------|------------|---------|
| 1          | Alfreds Futterkiste              | Maria Anders      | Obere Str. 57             | Berlin         | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados| Ana Trujillo     | Avda. de la Constitución 2222 | México D.F.  | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería          | Antonio Moreno    | Mataderos 2312            | México D.F.    | 05023      | Mexico  |



Și o selecție din tabelul `Suppliers`:

| `SupplierID` | `SupplierName`                    | Cont`actName    | `Address`                  | `City`           | `PostalCode` | `Country` |
|------------|---------------------------------|-----------------|--------------------------|----------------|-------------|---------|
| 1          | Exotic Liquid                   | Charlotte Cooper | 49 Gilbert St.           | Londona        | EC1 4SD     | UK      |
| 2          | New Orleans Cajun Delights      | Shelley Burke    | P.O. Box 78934           | New Orleans    | 70117       | USA     |
| 3          | Grandma Kelly's Homestead       | Regina Murphy    | 707 Oxford Rd.           | Ann Arbor      | 48104       | USA     |

## Exemple INSERT INTO SELECT

Copiați `Suppliers` în `Clients` (coloanele care nu sunt completate cu date vor conține `NULL`):

```sql
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers;
```

Copiați `Suppliers` în `Clients` (completați toate coloanele):

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
SELECT SupplierName, ContactName, Address, City, PostalCode, Country FROM Suppliers;
```
Copiați numai furnizorii germani în `Clients`:

```sql
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers
WHERE Country='Germany';
```

