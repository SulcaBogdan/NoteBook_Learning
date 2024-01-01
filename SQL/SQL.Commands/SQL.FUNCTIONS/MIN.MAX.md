# SQL FUNCTIILE MIN() SI MAX() 

## Funcțiile SQL `MIN()` și `MAX()`
Funcția `MIN()` returnează valoarea cea mai mică din coloana selectată.

Funcția `MAX()` returnează valoarea cea mai mare din coloana selectată.

```sql
SELECT MIN(Price)
FROM Products;
```

```sql
SELECT MAX(Price)
FROM Products;
```

## Sintaxa

```sql
SELECT MIN(column_name)
FROM table_name
WHERE condition;
```

```sql
SELECT MAX(column_name)
FROM table_name
WHERE condition;
```

| `ProductID` | `ProductName`                     | `SupplierID` | `CategoryID` | `Unit`                   | `Price` |
|-----------|---------------------------------|------------|------------|------------------------|-------|
| 1         | Chais                           | 1          | 1          | 10 boxes x 20 bags     | 18    |
| 2         | Chang                           | 1          | 1          | 24 - 12 oz bottles    | 19    |
| 3         | Aniseed Syrup                   | 1          | 2          | 12 - 550 ml bottles   | 10    |
| 4         | Chef Anton's Cajun Seasoning    | 2          | 2          | 48 - 6 oz jars         | 22    |
| 5         | Chef Anton's Gumbo Mix          | 2          | 2          | 36 boxes               | 21.35  |


## Setează Numele Coloanei (Alias)
Atunci când folosești `MIN()` sau `MAX()`, coloana returnată va avea numele `MIN`(field) sau `MAX`(field) în mod implicit. Pentru a atribui coloanei un nume nou, folosește cuvântul cheie `AS`:

```sql
SELECT MIN(Price) AS SmallestPrice
FROM Products;
```