# Sintaxa limbajului SQL

## SQL Statements
Majoritatea acțiunilor pe care trebuie să le efectuezi asupra unei baze de date se fac cu ajutorul instrucțiunilor SQL.

Instrucțiunile SQL constau din cuvinte cheie ușor de înțeles.

Următoarea instrucțiune SQL returnează toate înregistrările dintr-o tabelă numită "`Customers`":

```sql
SELECT * FROM Customers;
```

## Tabele de Bază de Date
O bază de date conține cel mai adesea una sau mai multe tabele. Fiecare tabel este identificat printr-un nume (de exemplu, "`Customers`" sau "`Orders`") și conține înregistrări (rânduri) cu date.

În acest tutorial, vom utiliza baza de date de exemplu Northwind (inclusă în MS Access și MS SQL Server).

Mai jos este o selecție din tabela "Customers" utilizată în exemple:

| `CustomerID` | `CustomerName`                   | `ContactName`       | `Address`                    | `City`          | `PostalCode` | `Country` |
|------------|--------------------------------|-------------------|----------------------------|---------------|------------|---------|
| 1          | Alfreds Futterkiste            | Maria Anders      | Obere Str. 57               | Berlin        | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería        | Antonio Moreno    | Mataderos 2312              | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn                 | Thomas Hardy      | 120 Hanover Sq.            | London        | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8            | Luleå         | S-958 22   | Sweden  |

Tabela de mai sus conține cinci înregistrări (una pentru fiecare client) și șapte coloane (`CustomerID`, `CustomerName`, `ContactName`, `Address`, `City`, `PostalCode` și `Country`).


### Ține Minte Că...

Cuvintele cheie SQL NU sunt sensibile la majuscule/minusculă: `select` este la fel cu `SELECT`. Este best practice sa se scrie cu `UPPERCASE`.

## `;` După Instrucțiunile SQL?

Unele sisteme de baze de date necesită un punct și virgulă la sfârșitul fiecărei instrucțiuni SQL.

Punctul și virgulă este modalitatea standard de a separa fiecare instrucțiune SQL în sistemele de baze de date care permit executarea mai multor instrucțiuni SQL în aceeași apel către server.

| Comanda             | Explicație                               |
|---------------------|------------------------------------------|
| `SELECT`            | extrage date dintr-o bază de date        |
| `UPDATE`            | actualizează date într-o bază de date    |
| `DELETE`            | șterge date dintr-o bază de date         |
| `INSERT INTO`       | introduce date noi într-o bază de date   |
| `CREATE DATABASE`   | creează o bază de date nouă               |
| `ALTER DATABASE`    | modifică o bază de date                   |
| `CREATE TABLE`      | creează o tabelă nouă                     |
| `ALTER TABLE`       | modifică o tabelă                        |
| `DROP TABLE`        | șterge o tabelă                          |
| `CREATE INDEX`      | creează un index (cheie de căutare)      |
| `DROP INDEX`        | șterge un index de la o tabelă           |


