# ALTER TABLE in SQL

Instrucțiunea `ALTER TABLE` este utilizată pentru a adăuga, șterge sau modifica coloane dintr-un tabel existent.

Instrucțiunea `ALTER TABLE` este, de asemenea, folosită pentru a adăuga și elimina diferite constrângeri pe un tabel existent.

## ALTER TABLE - ADD Coloană
Pentru a adăuga o coloană într-un tabel, utilizați următoarea sintaxă:

### Sintaxa

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

Următorul SQL adaugă o coloană `E-mail` la tabelul `Clients`:

```sql
ALTER TABLE Customers
ADD Email varchar(255);
```
## ALTER TABLE - DROP COLUMN
Pentru a șterge o coloană dintr-un tabel, utilizați următoarea sintaxă (observați că unele sisteme de baze de date nu permit ștergerea unei coloane):

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

Următorul SQL șterge coloana `E-mail` din tabelul `Clients`:

```sql
ALTER TABLE Customers
DROP COLUMN Email;
```
## ALTER TABLE - RENAME COLOANA
Pentru a redenumi o coloană dintr-un tabel, utilizați următoarea sintaxă:

### Sintaxa


```sql
ALTER TABLE table_name
RENAME COLUMN old_name to new_name;
```

## ALTER TABLE - ALTER/MODIFY DATATYPE
Pentru a schimba tipul de date al unei coloane dintr-un tabel, utilizați următoarea sintaxă:

### SQL Server / MS Access:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```
### My SQL / Oracle (versiunea anterioară 10G):

```sql
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

### Oracle 10G și versiuni ulterioare:

```sql
ALTER TABLE table_name
MODIFY column_name datatype;
```

## Exemplu SQL ALTER TABLE
Uită-te la tabelul `Persons`:

| `ID` | `LastName`  | `FirstName` | `Address`        | `City`      |
|----|-----------|-----------|----------------|-----------|
| 1  | Hansen    | Ola       | Timoteivn 10   | Sandnes   |
| 2  | Svendson  | Tove      | Borgvn 23      | Sandnes   |
| 3  | Pettersen | Kari      | Storgt 20      | Stavanger |


Acum dorim să adăugăm o coloană numită `DateOfBirth` în tabelul `Persons`.

Folosim următoarea instrucțiune SQL:

```sql
ALTER TABLE Persons
ADD DateOfBirth date;
```

Observați că noua coloană, `DateOfBirth`, este de tipul dată și va păstra o dată. Tipul de date specifică ce tip de date poate conține coloana. Pentru o referință completă a tuturor tipurilor de date disponibile în `MS Access`, `MySQL` și `SQL Server`, accesați referința noastră completă Tipuri de date.

Tabelul `Persons` va arăta acum astfel:

| `ID` | `LastName`  | `FirstName` | `Address`        | `City`      | `DateOfBirth` |
|----|-----------|-----------|----------------|-----------|-------------|
| 1  | Hansen    | Ola       | Timoteivn 10   | Sandnes   |             |
| 2  | Svendson  | Tove      | Borgvn 23      | Sandnes   |             |
| 3  | Pettersen | Kari      | Storgt 20      | Stavanger |             |


## Exemplu de modificare a tipului de date
Acum dorim să schimbăm tipul de date al coloanei numită `DateOfBirth` din tabelul `Persons`.

Folosim următoarea instrucțiune SQL:

```sql
ALTER TABLE Persons
ALTER COLUMN DateOfBirth year;
```

Observați că coloana `DateOfBirth` este acum de tipul an și va conține un an într-un format de două sau patru cifre.

## Exemplu DROP COLUMN 
În continuare, dorim să ștergem coloana numită `DateOfBirth` din tabelul `Persons`.

Folosim următoarea instrucțiune SQL:

```sql
ALTER TABLE Persons
DROP COLUMN DateOfBirth;
```

Tabelul `Persons` va arăta acum astfel:

| `ID` | `LastName`  | `FirstName` | `Address`        | `City`      |
|----|-----------|-----------|----------------|-----------|
| 1  | Hansen    | Ola       | Timoteivn 10   | Sandnes   |
| 2  | Svendson  | Tove      | Borgvn 23      | Sandnes   |
| 3  | Pettersen | Kari      | Storgt 20      | Stavanger |


