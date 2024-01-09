# SQL UNIQUE Constraint
`UNIQUE Constraint` asigură că toate valorile dintr-o coloană sunt diferite.

Atât `UNIQUE Constraints`, cât și `PRIMARY KEY` oferă o garanție pentru unicitatea unei coloane sau a unui set de coloane.

O constrângere `PRIMARY KEY Constraint` are automat o constrângere `UNIQUE`.

Cu toate acestea, puteți avea multe constrângeri `UNIQUE` pe tabel, dar o singură constrângere `PRIMARY KEY` per tabel.

## Constrângere SQL UNIQUE pe CREATE TABLE
Următorul SQL creează o constrângere `UNICĂ` pe coloana `ID` atunci când este creat tabelul `Persons`:

### SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Persons (
    ID int NOT NULL UNIQUE,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

### MySQL:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    UNIQUE (ID)
);
```

Pentru a denumi o `UNIQUE Constraint` și pentru a defini un `UNIQUE Constraint` pe mai multe coloane, utilizați următoarea sintaxă SQL:

### MySQL / SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT UC_Person UNIQUE (ID,LastName)
)
```

## SQL UNIQUE Constraint pe ALTER TABLE
Pentru a crea un `UNIQUE Constraint` pe coloana `ID` atunci când tabelul este deja creat, utilizați următorul SQL:

### MySQL / SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
ADD UNIQUE (ID);
```
Pentru a denumi o `UNIQUE Constraint` și pentru a defini un `UNIQUE Constraint` pe mai multe coloane, utilizați următoarea sintaxă SQL:

### SQL / SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);
```

## DROP a UNIQUE Constraint
Pentru a elimina un `UNIQUE Constraint`, utilizați următorul SQL:

### MySQL:

```sql
ALTER TABLE Persons
DROP INDEX UC_Person;
```

### SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
DROP CONSTRAINT UC_Person;
```