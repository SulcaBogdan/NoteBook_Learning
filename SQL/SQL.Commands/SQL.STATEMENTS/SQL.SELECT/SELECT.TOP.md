# SELECT TOP

## Clauza SQL SELECT TOP

Clauza `SELECT TOP` este folosită pentru a specifica numărul de înregistrări de returnat.

Clauza `SELECT TOP` este utilă pentru tabele mari cu mii de înregistrări. Returnarea unui număr mare de înregistrări poate afecta performanța.

```sql
SELECT TOP 3 * FROM Customers;
```

 **Notă**: Nu toate sistemele de baze de date suportă clauza `SELECT TOP`. MySQL folosește clauza `LIMIT` pentru a selecta un număr limitat de înregistrări, în timp ce Oracle utilizează `FETCH FIRST` n `ROWS ONLY` și `ROWNUM`.

 ## Sintaxă pentru SQL Server / MS Access:

```sql
SELECT TOP number|percent column_name(s)
FROM table_name
WHERE condition;
```

## Sintaxă pentru MySQL:

```sql
SELECT column_name(s)
FROM table_name
WHERE condition
LIMIT number;
```

## Sintaxă pentru Oracle 12:

```sql
SELECT column_name(s)
FROM table_name
ORDER BY column_name(s)
FETCH FIRST number ROWS ONLY;
```

## Sintaxă veche pentru Oracle:

```sql
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number;
```

## Sintaxă veche pentru Oracle (cu ORDER BY):

```sql
SELECT *
FROM (SELECT column_name(s) FROM table_name ORDER BY column_name(s))
WHERE ROWNUM <= number;
```

| `CustomerID` | `CustomerName`                    | `ContactName`        | `Address`                      | `City`          | `PostalCode` | `Country` |
|------------|----------------------------------|--------------------|------------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste             | Maria Anders       | Obere Str. 57                | Berlin        | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo       | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería         | Antonio Moreno     | Mataderos 2312               | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                  | Thomas Hardy       | 120 Hanover Sq.              | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp               | Christina Berglund | Berguvsvägen 8               | Luleå         | S-958 22   | Sweden  |



