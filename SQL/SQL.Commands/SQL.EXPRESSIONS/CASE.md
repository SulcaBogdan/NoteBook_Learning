# CASE in SQL


Expresia `CASE` trece prin condiții și returnează o valoare atunci când prima condiție este îndeplinită (ca o instrucțiune `if-then-else`). Deci, odată ce o condiție este adevărată, se va opri citirea și va returna rezultatul. Dacă nu sunt adevărate condiții, returnează valoarea din clauza `ELSE`.

Dacă nu există nicio parte `ELSE` și nicio condiție nu este adevărată, returnează `NULL`.

## Sintaxa CASE

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;
```

Mai jos este o selecție din tabelul `OrderDetails` din baza de date eșantion `Northwind`:

| `OrderDetailID` | `OrderID` | `ProductID` | `Quantity` |
|---------------|---------|------------|----------|
| 1             | 10248   | 11         | 12       |
| 2             | 10248   | 42         | 10       |
| 3             | 10248   | 72         | 5        |
| 4             | 10249   | 14         | 9        |
| 5             | 10249   | 51         | 40       |


## Exemplu CASE

Următorul SQL trece prin condiții și returnează o valoare atunci când prima condiție este îndeplinită:

```sql
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```

Următorul SQL va ordona clienții în funcție de oraș. Cu toate acestea, dacă `City` este `NULL`, atunci ordonați după țară:

```sql
SELECT CustomerName, City, Country
FROM Customers
ORDER BY
(CASE
    WHEN City IS NULL THEN Country
    ELSE City
END);
```


