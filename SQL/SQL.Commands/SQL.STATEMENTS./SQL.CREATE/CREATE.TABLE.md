# CREATE TABLE in SQL

Instrucțiunea `CREATE TABLE` este utilizată pentru a crea un tabel nou într-o bază de date.

## Sintaxă

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```

Parametrii coloanei specifică numele coloanelor din tabel.

Parametrul datatype specifică tipul de date pe care coloana îl poate deține (de exemplu, varchar, întreg, dată etc.).

`Nota`: **Pentru o prezentare generală a tipurilor de date disponibile, accesați Referința noastră completă pentru tipurile de date.**

## Exemplu SQL CREATE TABLE 
Următorul exemplu creează un tabel numit `Persons` care conține cinci coloane: `PersonID`, `LastName`, `FirstName`, `Address` și `City`:

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```

Coloana `PersonID` este de tip `int` și va conține un număr întreg.

`Coloanele` `LastName`, `FirstName`, `Address` și `City` sunt de tip `varchar` și vor conține caractere, iar lungimea maximă pentru aceste câmpuri este de 255 de caractere.

Tabelul gol `Persons` va arăta acum astfel:

| PersonID | LastName | FirstName | Address | City |
|----------|----------|-----------|---------|------|
|          |          |           |         |      |


`Nota`: Tabelul `Persons` gol poate fi acum completat cu date cu instrucțiunea SQL `INSERT INTO`.

## Creați un tabel folosind un alt tabel
O copie a unui tabel existent poate fi creată și folosind `CREATE TABLE`.

Noul tabel primește aceleași definiții de coloană. Pot fi selectate toate coloanele sau anumite coloane.

Dacă creați un tabel nou folosind un tabel existent, noul tabel va fi completat cu valorile existente din tabelul vechi.

## Sintaxă


```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
```
Următorul SQL creează un nou tabel numit `TestTables` (care este o copie a tabelului `Clients`):

```sql
CREATE TABLE TestTable AS
SELECT customername, contactname
FROM customers;
```

