# SQL COUNT

Funcția `COUNT()` returnează numărul de rânduri care îndeplinesc un criteriu specificat.

```sql
SELECT COUNT(*)
FROM Products;
```

## Sintaxa

```sql
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```

| `ProductID` | `ProductName`                     | `SupplierID` | `CategoryID` | `Unit`                  | `Price` |
|-----------|---------------------------------|------------|------------|-----------------------|-------|
| 1         | Chais                           | 1          | 1          | 10 boxes x 20 bags    | 18    |
| 2         | Chang                           | 1          | 1          | 24 - 12 oz bottles   | 19    |
| 3         | Aniseed Syrup                   | 1          | 2          | 12 - 550 ml bottles  | 10    |
| 4         | Chef Anton's Cajun Seasoning    | 2          | 2          | 48 - 6 oz jars        | 22    |
| 5         | Chef Anton's Gumbo Mix          | 2          | 2          | 36 boxes              | 21.35 |

## Adauga o clauza WHERE pentru a specifica conditii:

```sql
SELECT COUNT(ProductID)
FROM Products
WHERE Price > 20;
```

## Specifica coloana

Poti specifica un nume de coloana in locul simbolului asterix (`*`).

Daca specifici o coloana in loc de (`*`), valorile NULL nu vor fi luate in considerare.

```sql
SELECT COUNT(ProductName)
FROM Products;
```
## Ignora duplicate

Poti ignora duplicatele folosind cuvantul-cheie `DISTINCT` in functia `COUNT`.

Daca se specifica `DISTINCT`, randurile cu aceeasi valoare pentru coloana specificata vor fi numarate ca una singura.

```sql
SELECT COUNT(DISTINCT Price)
FROM Products;
```

## Foloseste un alias

Da un nume coloanei numarate folosind cuvantul-cheie `AS`.

```sql
SELECT COUNT(*) AS [number of records]
FROM Products;
```




