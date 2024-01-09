# SQL DELETE

## SQL DELETE Statement

The DELETE statement is used to delete existing records in a table.

```sql
DELETE FROM table_name
WHERE condition;
```

### ATENȚIE: Fii atent atunci când ștergi înregistrările dintr-o tabelă!

Observă clauza `WHERE` în instrucțiunea `DELETE`. Clauza `WHERE` specifică care înregistrări trebuie șterse. Dacă omiti clauza `WHERE`, vor fi șterse toate înregistrările din tabel!

## Tabel Customers

| CustomerID | CustomerName                   | ContactName       | Address                    | City          | PostalCode | Country |
|------------|---------------------------------|-------------------|----------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders      | Obere Str. 57              | Berlin         | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería         | Antonio Moreno    | Mataderos 2312             | México D.F.    | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.            | London         | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8            | Luleå          | S-958 22   | Sweden  |



## Exemplu SQL DELETE

Următorul statement SQL șterge clientul "Alfreds Futterkiste" din tabela "Customers".

```sql
DELETE FROM Customers 
WHERE CustomerName='Alfreds Futterkiste';
```

## Tabel "Customers"

| CustomerID | CustomerName                  | ContactName     | Address                        | City          | PostalCode | Country |
|------------|-------------------------------|------------------|--------------------------------|---------------|------------|---------|
| 2          | Ana Trujillo Emparedados y... | Ana Trujillo     | Avda. de la Constitución 2222  | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería       | Antonio Moreno   | Mataderos 2312                 | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                | Thomas Hardy     | 120 Hanover Sq.                | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp            | Christina Berglund | Berguvsvägen 8               | Luleå         | S-958 22   | Sweden  |


## Șterge toate înregistrările

Pentru a șterge toate rândurile dintr-o tabelă fără a șterge însă însăși tabela. Acest lucru înseamnă că structura tabelului, atributele și indexurile vor rămâne intacte:

```sql
DELETE FROM table_name;
```

Următoarea declarație SQL șterge toate rândurile din tabela "`Customers`", fără a șterge însă tabela:

```sql
DELETE FROM Customers;
```

Pentru a șterge complet o tabelă, folosește declarația `DROP TABLE`:

```sql
DROP TABLE Customers;
```

