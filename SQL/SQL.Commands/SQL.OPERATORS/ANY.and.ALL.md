# ANY si ALL in SQL

Operatorii `ANY` și `ALL` vă permit să efectuați o comparație între o singură valoare de coloană și un interval de alte valori.

## Operatorul SQL ANY

- returnează o valoare booleană ca rezultat;
- returnează `TRUE` dacă ORICA dintre valorile subinterogării îndeplinește condiția.
  
**`ANY` înseamnă că condiția va fi adevărată dacă operația este adevărată pentru oricare dintre valorile din interval.**

## Sintaxa ANY

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name operator ANY
  (SELECT column_name
  FROM table_name
  WHERE condition);
```

`Notă`: **operatorul trebuie să fie un operator de comparare standard `(=,` `<>`, `!=`, `>`, `>=`, `<` sau `<=`).**

## Operatorul SQL ALL

- returnează o valoare booleană ca rezultat
- returnează `TRUE` dacă `ALL` valorile subinterogării îndeplinesc condiția
- este utilizat cu instrucțiunile `SELECT`, `WHERE` și `HAVING`
`ALL` înseamnă că condiția va fi adevărată numai dacă operația este adevărată pentru toate valorile din interval.

## Sintaxa ALL cu SELECT

```sql
SELECT ALL column_name(s)
FROM table_name
WHERE condition;
```

## Sintaxa ALL cu WHERE sau HAVING

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name operator ALL
  (SELECT column_name
  FROM table_name
  WHERE condition);
```

`Notă`: **operatorul trebuie să fie un operator de comparare standard (`=`, `<>`, `!=`, `>`, `>=`, `<` sau `<=`).**

Mai jos este o selecție din tabelul `Products` din baza de date exemplu `Northwind`:

Și o selecție din tabelul `OrderDetails`:


| `OrderDetailID` | `OrderID` | `ProductID` | `Quantity` |
|---------------|---------|------------|----------|
| 1             | 10248   | 11         | 12       |
| 2             | 10248   | 42         | 10       |
| 3             | 10248   | 72         | 5        |
| 4             | 10249   | 14         | 9        |
| 5             | 10249   | 51         | 40       |
| 6             | 10250   | 41         | 10       |
| 7             | 10250   | 51         | 35       |
| 8             | 10250   | 65         | 15       |
| 9             | 10251   | 22         | 6        |
| 10            | 10251   | 57         | 15       |

## Exemple ANY 

Următoarea instrucțiune SQL listează `ProductName` dacă găsește `ANY` înregistrări în tabelul `OrderDetails` are o cantitate egală cu 10 (aceasta va returna `TRUE` deoarece coloana `Quantity` are unele valori de 10):

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10);
```

Următoarea instrucțiune SQL listează `ProductName` dacă găsește `ANY` records în tabelul `OrderDetails` are o cantitate mai mare de 99 (aceasta va returna `TRUE` deoarece coloana `Quantity` are unele valori mai mari de 99):

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity > 99);
```

Următoarea instrucțiune SQL listează `ProductName` dacă găsește `ANY` înregistrări în tabelul `OrderDetails` are o cantitate mai mare de 1000 (aceasta va returna `FALSE` deoarece coloana `Quantity` nu are valori mai mari de 1000):

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity > 1000);
```

## Exemple ALL

Următoarea instrucțiune SQL listează `ALL` numele produselor:

```SQL
SELECT ALL ProductName
FROM Products
WHERE TRUE;
```

Următoarea instrucțiune SQL listează `ProductName` dacă `ALL` înregistrările din tabelul `OrderDetails` au `Quantity` egală cu 10. Aceasta va returna, desigur, `FALS` deoarece coloana `Quantity` are multe valori diferite (nu doar valoarea 10):


```SQL
SELECT ProductName
FROM Products
WHERE ProductID = ALL
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10);
```
