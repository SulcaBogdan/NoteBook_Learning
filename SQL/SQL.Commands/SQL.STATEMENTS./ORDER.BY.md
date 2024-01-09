# ORDER BY SQL

## Instrucțiunea SQL ORDER BY
Cuvântul cheie `ORDER BY` este folosit pentru a sorta setul de rezultate în ordine crescătoare sau descrescătoare.


```sql
SELECT * FROM Products
ORDER BY Price;
```

## Sintaxa

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```

| `ProductID` | `ProductName`                   | `SupplierID` | `CategoryID` | `Unit`                   | `Price` |
|-----------|-------------------------------|------------|------------|------------------------|-------|
| 1         | Chais                         | 1          | 1          | 10 boxes x 20 bags     | 18    |
| 2         | Chang                         | 1          | 1          | 24 - 12 oz bottles     | 19    |
| 3         | Aniseed Syrup                 | 1          | 2          | 12 - 550 ml bottles    | 10    |
| 4         | Chef Anton's Cajun Seasoning  | 2          | 2          | 48 - 6 oz jars         | 22    |
| 5         | Chef Anton's Gumbo Mix        | 2          | 2          | 36 boxes               | 21.35 |


## DESC
Cuvântul cheie `ORDER BY` sortează în mod implicit înregistrările în ordine crescătoare. Pentru a sorta înregistrările în ordine descrescătoare, folosește cuvântul cheie `DESC`.

```sql
SELECT * FROM Products
ORDER BY Price DESC;
```

## Ordine Alfabetică
Pentru valori de tip șir de caractere, cuvântul cheie `ORDER BY` va ordona în mod alfabetic:


```sql
SELECT * FROM Products
ORDER BY ProductName;
```

## Alfabetic DESC
Pentru a sorta tabela în mod invers alfabetic, folosește cuvântul cheie `DESC`:

```sql
SELECT * FROM Products
ORDER BY ProductName DESC;
```

## ORDER BY Mai Multe Coloane
Următoarea instrucțiune SQL selectează toți clienții din tabela "`Customers`", sortați după coloanele "`Country`" și "`CustomerName`". Acest lucru înseamnă că ordonează după țară, dar dacă unele rânduri au aceeași țară, le ordonează după `CustomerName`:

```sql
SELECT * FROM Customers
ORDER BY Country, CustomerName;
```


## Utilizând Atât ASC, Cât și DESC
Următoarea instrucțiune SQL selectează toți clienții din tabela "`Customers`", sortați în ordine crescătoare după coloana "`Country`" și în ordine descrescătoare după coloana "`CustomerName`":

```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```
