# SELF JOIN in SQL

O alăturare automată este o alăturare obișnuită, dar tabelul este alăturat cu el însuși.

## Sintaxa Self Join
```sql
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;
```

`T1` și `T2` sunt aliasuri de tabel diferite pentru același tabel.

În acest tutorial vom folosi binecunoscuta bază de date mostre `Northwind`.

Mai jos este o selecție din tabelul `Clients`:

| `CustomerID` | `CustomerName`                      | `ContactName`    | `Address`                          | `City`           | `PostalCode` | `Country` |
|------------|----------------------------------|-----------------|----------------------------------|----------------|------------|---------|
| 1          | Alfreds Futterkiste              | Maria Anders    | Obere Str. 57                    | Berlin         | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados| Ana Trujillo    | Avda. de la Constitución 2222    | México D.F.    | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería          | Antonio Moreno  | Mataderos 2312                   | México D.F.    | 05023      | Mexico  |


### SELF JOIN SQL Exemplu:

Următoarea instrucțiune SQL corespunde clienților care sunt din același oraș:

```sql
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City
ORDER BY A.City;
```

