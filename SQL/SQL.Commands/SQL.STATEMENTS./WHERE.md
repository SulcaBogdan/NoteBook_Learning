# WHERE Clause

## Instrucțiunea WHERE
Clausa `WHERE` este folosită pentru a filtra înregistrările.

Este folosită pentru a extrage doar înregistrările care îndeplinesc o condiție specificată.

```sql
SELECT * FROM Customers
WHERE Country='Mexico';
```

## Sintaxa

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
**Notă:** Clausa `WHERE` nu este folosită doar în instrucțiunile `SELECT`, ci și în `UPDATE`, `DELETE`, etc.!

| `CustomerID` | `CustomerName`                   | `ContactName`       | `Address`                    | `City`          | `PostalCode` | `Country` |
|------------|--------------------------------|-------------------|----------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders      | Obere Str. 57               | Berlin        | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno    | Mataderos 2312              | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.            | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8            | Luleå         | S-958 22   | Sweden  |



## Câmpuri Text vs. Câmpuri Numerice
SQL necesită ghilimele simple în jurul valorilor text (majoritatea sistemelor de baze de date permit și ghilimele duble).

Cu toate acestea, câmpurile numerice nu ar trebui închise în ghilimele:

```sql
SELECT * FROM Customers
WHERE CustomerID=1;
```

## Operatori în Clausa WHERE
Poți utiliza alți operatori în afara operatorului = pentru a filtra căutarea.

```sql
SELECT * FROM Customers
WHERE CustomerID > 80;
```

| Operator | Descriere                                    |
|----------|----------------------------------------------|
| `=`      | Egal                                         |
| `>`      | Mai mare decât                                |
| `<`      | Mai mic decât                                 |
| `>=`     | Mai mare sau egal                             |
| `<=`     | Mai mic sau egal                              |
| `<>` sau `!=` | Diferit. Notă: În unele versiuni de SQL, acest operator poate fi scris și ca != |
| `BETWEEN`| Între un anumit interval                      |
| `LIKE`   | Caută un șablon                              |
| `IN`     | Pentru a specifica mai multe valori posibile pentru o coloană |


