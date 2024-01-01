# AVG SQL

## Funcția SQL AVG().
Funcția `AVG()` returnează valoarea medie a unei coloane numerice.

```sql
SELECT AVG(Price)
FROM Products;
```

**Notă**: valorile `NULL` sunt ignorate.

## Sintaxa

```sql
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```



| `ProductID` | `ProductName`                 | `SupplierID` | `CategoryID` | `Unit`                   | `Price` |
|-----------|-----------------------------|-------------|------------|------------------------|-------|
| 1         | Chais                       | 1           | 1          | 10 boxes x 20 bags     | 18    |
| 2         | Chang                       | 1           | 1          | 24 - 12 oz bottles     | 19    |
| 3         | Aniseed Syrup               | 1           | 2          | 12 - 550 ml bottles    | 10    |
| 4         | Chef Anton's Cajun Seasoning | 2           | 2          | 48 - 6 oz jars         | 22    |
| 5         | Chef Anton's Gumbo Mix      | 2           | 2          | 36 boxes               | 21.3  |

## Adăugați o clauză WHERE:

Puteți adăuga o clauză `WHERE` pentru a specifica condiții:

```SQL
SELECT AVG(Price)
FROM Products
WHERE CategoryID = 1;
```

## Utilizați un alias

Dați un nume coloanei `AVG` utilizând cuvântul cheie `AS`.

```SQL
SELECT AVG(Price) AS [average price]
FROM Products;
```

## Mai mare decât medie

Pentru a lista toate înregistrările cu un preț mai mare decât media, putem folosi funcția `AVG()` într-o subinterogare:

```sql
SELECT * FROM Products
WHERE price > (SELECT AVG(price) FROM Products);
```