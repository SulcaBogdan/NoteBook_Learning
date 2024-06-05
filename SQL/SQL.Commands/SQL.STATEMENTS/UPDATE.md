# SQL UPDATE 

## Operatorul UPDATE
Operatorul `UPDATE` este folosit pentru a modifica înregistrările existente într-o tabelă.

### Sintaxa UPDATE

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
**Notă**: Fii atent atunci când actualizezi înregistrările într-o tabelă! Observă clauza `WHERE` în instrucțiunea `UPDATE`. Clauza `WHERE` specifică care înregistrare sau înregistrări trebuie actualizate. Dacă omiti clauza `WHERE`, vor fi actualizate toate înregistrările din tabel!


| `CustomerID` | `CustomerName`                   | `ContactName`        | `Address`             | `City`              | `PostalCode` | `Country` |
|------------|--------------------------------|--------------------|---------------------|-------------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders       | Obere Str. 57        | Berlin            | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo    | Avda. de la Constitución 2222 | México D.F.  | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno     | Nuevo Address 123   | Ciudad de México  | 12345      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy       | 120 Hanover Sq.     | London            | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8      | Luleå             | S-958 22   | Sweden  |


## UPDATE Tabel
Instrucțiunea SQL următoare actualizează primul client (CustomerID = 1) cu un `new contact person` și un `new city`.

```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;
```

### Selecția din tabelul "Customers" va arăta acum în felul următor:

| CustomerID | CustomerName                   | ContactName       | Address               | City          | PostalCode | Country |
|------------|--------------------------------|-------------------|-----------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Alfred Schmidt    | Obere Str. 57         | Frankfurt     | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo     | Avda. de la Constitución 2222 | México D.F.  | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno    | Mataderos 2312        | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.       | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8      | Luleå         | S-958 22   | Sweden  |

## Actualizare mai multe înregistrări

Este clauza WHERE care determină câte înregistrări vor fi actualizate.

Următorul instrucțiune SQL va actualiza ContactName la "Juan" pentru toate înregistrările unde țara este "Mexico":

```sql
UPDATE Customers
SET ContactName = 'Juan'
WHERE Country = 'Mexico';
```

| `CustomerID` | `CustomerName`             | `ContactName`        | `Address`                   | `City`       | `PostalCode` | `Country` |
|------------|--------------------------|---------------------|---------------------------|------------|------------|---------|
| 1          | Alfreds Futterkiste      | Alfred Schmidt      | Obere Str. 57              | Frankfurt  | 12209      | Germany |
| 2          | Ana Trujillo Emparedados | Juan                | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería  | Juan                | Mataderos 2312            | México D.F. | 05023      | Mexico  |
| 4          | Around the Horn           | Thomas Hardy        | 120 Hanover Sq.           | London     | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp       | Christina Berglund  | Berguvsvägen 8            | Luleå      | S-958 22   | Sweden  |

## Atenție la Actualizare!

Fiți atenți atunci când actualizați înregistrările. Dacă omiteți clauza `WHERE`, TOATE înregistrările vor fi actualizate!

```sql
UPDATE Customers
SET ContactName='Juan';
```
### Customer Table Update

| CustomerID | CustomerName                 | ContactName | Address                 | City       | PostalCode | Country |
|------------|------------------------------|-------------|-------------------------|------------|------------|---------|
| 1          | Alfreds Futterkiste          | Juan        | Obere Str. 57           | Frankfurt  | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Juan        | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería      | Juan        | Mataderos 2312          | México D.F. | 05023      | Mexico  |
| 4          | Around the Horn               | Juan        | 120 Hanover Sq.         | London     | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp           | Juan        | Berguvsvägen 8          | Luleå      | S-958 22   | Sweden  |









