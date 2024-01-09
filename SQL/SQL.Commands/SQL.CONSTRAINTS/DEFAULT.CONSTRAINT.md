# SQL DEFAULT Constraint

`DEFAULT Constraint` este utilizată pentru a seta o valoare implicită pentru o coloană.

Valoarea implicită va fi adăugată la toate înregistrările noi, dacă nu este specificată nicio altă valoare.

## SQL DEFAULT on CREATE TABLE

Următorul SQL setează o valoare `DEFAULT` pentru coloana `City` atunci când este creat tabelul `Persons`:

### My SQL / SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255) DEFAULT 'Sandnes'
);
```

`DEFAULT Constraint` poate fi folosită și pentru a introduce valori de sistem, folosind funcții precum `GETDATE()`:

```sql
CREATE TABLE Orders (
    ID int NOT NULL,
    OrderNumber int NOT NULL,
    OrderDate date DEFAULT GETDATE()
);
```

## SQL DEFAULT on ALTER TABLE

Pentru a crea un `DEFAULT Constraint `pe coloana `City` atunci când tabelul este deja creat, utilizați următorul SQL:

### MySQL:

```sql
ALTER TABLE Persons
ALTER City SET DEFAULT 'Sandnes';
```

### SQL Server:

```sql
ALTER TABLE Persons
ADD CONSTRAINT df_City
DEFAULT 'Sandnes' FOR City;
```

### MS Access:

```sql
ALTER TABLE Persons
ALTER COLUMN City SET DEFAULT 'Sandnes';
```

### Oracle:

```sql
ALTER TABLE Persons
MODIFY City DEFAULT 'Sandnes';
```

## DROP a DEFAULT Constraint

Pentru a elimina un `DEFAULT Constraint`, utilizați următorul SQL:


### MySQL:

```sql
ALTER TABLE Persons
ALTER City DROP DEFAULT;
```

### SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
ALTER COLUMN City DROP DEFAULT;
```
### SQL Server:

```sql
ALTER TABLE Persons
ALTER COLUMN City DROP DEFAULT;
```