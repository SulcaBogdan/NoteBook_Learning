# SUM SQL

## Functia SQL SUM()

Functia `SUM()` returneaza suma totala a unei coloane numerice.

```sql
SELECT SUM(Quantity)
FROM OrderDetails;
```

## Sintaxa

```sql
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```

## Tabelul OrderDetails

| OrderDetailID | OrderID | ProductID | Quantity |
|---------------|---------|-----------|----------|
| 1             | 10248   | 11        | 12       |
| 2             | 10248   | 42        | 10       |
| 3             | 10248   | 72        | 5        |
| 4             | 10249   | 14        | 9        |
| 5             | 10249   | 51        | 40       |



## Adăugați o clauză WHERE:

Puteți adăuga o clauză `WHERE` pentru a specifica condiții:

```sql
SELECT SUM(Quantity)
FROM OrderDetails
WHERE ProductId = 11;
```

## Utilizați un alias

Dați un nume coloanei rezumate utilizând cuvântul cheie `AS`.

```sql
SELECT SUM(Quantity) AS total
FROM OrderDetails;
```

## SUM() Cu o expresie
Parametrul din interiorul funcției` SUM()` poate fi, de asemenea, o expresie.

Dacă presupunem că fiecare produs din coloana `OrderDetails` costă `10 dolari`, putem găsi câștigurile totale în dolari înmulțind fiecare cantitate cu `10`:

```sql
SELECT SUM(Quantity * 10)
FROM OrderDetails;
```
De asemenea, putem asocia tabelul `OrderDetails` la tabelul `Products` pentru a găsi suma reală, în loc să presupunem că este de `10 dolari`:


```sql
SELECT SUM(Price * Quantity)
FROM OrderDetails
LEFT JOIN Products ON OrderDetails.ProductID = Products.ProductID;
```