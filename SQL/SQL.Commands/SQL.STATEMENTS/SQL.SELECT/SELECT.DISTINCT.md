# SELECT DISTINCT SQL

## Instrucțiunea SQL SELECT DISTINCT
Instrucțiunea `SELECT DISTINCT` este folosită pentru a returna doar valori distincte (diferite).

```sql
SELECT DISTINCT Country 
FROM Customers;
```

## Sintaxa

```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

Într-o tabelă, o coloană conține adesea multe valori duplicate; iar uneori dorești doar să listezi valorile diferite (distincte).


| `CustomerID` | `CustomerName`                   | `ContactName`       | `Address`                    | `City`          | `PostalCode` | `Country` |
|------------|--------------------------------|-------------------|----------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders      | Obere Str. 57               | Berlin        | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno    | Mataderos 2312              | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.            | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8            | Luleå         | S-958 22   | Sweden  |


## Exemplu SELECT fără DISTINCT
Dacă omiți cuvântul `DISTINCT`, instrucțiunea SQL returnează valoarea "`Country`" din toate înregistrările tabelului "`Customers`":

```sql
SELECT Country 
FROM Customers;
```

## COUNT Distinct
Prin utilizarea cuvântului cheie `DISTINCT` într-o funcție numită `COUNT`, putem returna numărul de țări diferite.

**Notă:** `COUNT(DISTINCT column_name)` nu este suportat în bazele de date Microsoft Access.

```sql
SELECT Count(*) AS DistinctCountries
FROM (SELECT DISTINCT Country FROM Customers);
```



