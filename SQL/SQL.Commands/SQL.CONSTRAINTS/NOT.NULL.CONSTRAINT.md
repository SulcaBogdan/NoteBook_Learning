# SQL NOT NULL Constraint

În mod implicit, o coloană poate conține valori `NULL`.

`NOT NULL Constraint` impune ca o coloană să `NU` accepte valori `NULL`.

Acest lucru impune ca un câmp să conțină întotdeauna o valoare, ceea ce înseamnă că nu puteți introduce o înregistrare nouă sau nu puteți actualiza o înregistrare fără a adăuga o valoare acestui câmp.

## SQL NOT NULL pe CREATE TABLE
Următorul SQL asigură că coloanele `ID`, `LastName` și `FirstName` NU vor accepta valori `NULL` atunci când este creat tabelul `Persons`:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

## SQL NOT NULL pe ALTER TABLE
Pentru a crea un `NOT NULL Constraint` pe coloana `Age` când tabelul `Persons` este deja creat, utilizați următorul SQL:

### SQL Server / MS Access:

```sql
ALTER TABLE Persons
ALTER COLUMN Age int NOT NULL;
```

### My SQL / Oracle (versiunea anterioară 10G):

```sql
ALTER TABLE Persons
MODIFY COLUMN Age int NOT NULL;
```
### Oracle 10G și versiuni ulterioare:

```sql
ALTER TABLE Persons
MODIFY Age int NOT NULL;
```

