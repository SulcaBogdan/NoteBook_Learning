# SQL CHECK Constraint

`CHECK Constraint` este utilizată pentru a limita intervalul de valori care poate fi plasat într-o coloană.

Dacă definiți un `CHECK Constraint` pe o coloană, aceasta va permite numai anumite valori pentru această coloană.

Dacă definiți un `CHECK Constraint` pe un tabel, aceasta poate limita valorile din anumite coloane pe baza valorilor din alte coloane din rând.

## SQL CHECK on CREATE TABLE

Următorul SQL creează un `CHECK Constraint`  pe coloana `Age` atunci când este creat tabelul `Persons`.` CHECK Constraint` asigură că vârsta unei persoane trebuie să fie de 18 ani sau mai mult:

### MySql

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (Age>=18)
);
```

### SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int CHECK (Age>=18)
);
```

Pentru a permite denumirea unui `CHECK Constraint` și pentru a defini un `CHECK Constraint` pe mai multe coloane, utilizați următoarea sintaxă SQL:


### MySQL / SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255),
    CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
);
```

## SQL CHECK on ALTER TABLE

Pentru a crea un `CHECK Constraint` pe coloana `Age` când tabelul este deja creat, utilizați următorul SQL:

### MySQL / SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
ADD CHECK (Age>=18);
```

Pentru a permite denumirea unui `CHECK Constraint` și pentru a defini un `CHECK Constraint` pe mai multe coloane, utilizați următoarea sintaxă SQL:

### MySQL / SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
ADD CONSTRAINT CHK_PersonAge CHECK (Age>=18 AND City='Sandnes');
```

## DROP a CHECK Constraint

Pentru a elimina un `CHECK Constraint`, utilizați următorul SQL:

### SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
DROP CONSTRAINT CHK_PersonAge;
```

### MySQL:

```sql
ALTER TABLE Persons
DROP CHECK CHK_PersonAge;
```



