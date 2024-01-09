# SQL PRIMARY KEY Constraint


`PRIMARY KEY Constraint` identifică în mod unic fiecare înregistrare dintr-un tabel.

`PRIMARY KEY`'s trebuie să conțină valori `UNIQUE` și nu pot conține valori `NULL`.

Un tabel poate avea doar un `PRIMARY KEY`; iar în tabel, această cheie primară poate consta dintr-o singură sau mai multe coloane (câmpuri).

## SQL PRIMARY KEY on CREATE TABLE
Următorul SQL creează un `PRIMARY KEY` pe coloana `ID` atunci când este creat tabelul `Persons`:

### MySQL:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    PRIMARY KEY (ID)
);
```

### SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Persons (
    ID int NOT NULL PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

Pentru a permite denumirea unei `PRIMARY KEY Constraint` și pentru a defini o `PRIMARY KEY Constraint` pe mai multe coloane, utilizați următoarea sintaxă SQL:

### MySQL / SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)
);
```

`Notă`: În exemplul de mai sus există doar un `PRIMARY KEY` (**PK_Person**). Cu toate acestea, VALUE a cheii primare este alcătuită din DOUĂ COLOANE (ID + Nume).

## SQL PRIMARY KEY pe ALTER TABLE
Pentru a crea o `PRIMARY KEY Constraint` pe coloana `ID` atunci când tabelul este deja creat, utilizați următorul SQL:

### MySQL / SQL Server / Oracle / MS Access:


```sql
ALTER TABLE Persons
ADD PRIMARY KEY (ID);
```

Pentru a permite denumirea unei `PRIMARY KEY Constraint `și pentru a defini o `PRIMARY KEY Constraint` pe mai multe coloane, utilizați următoarea sintaxă SQL:

### MySQL / SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
ADD CONSTRAINT PK_Person PRIMARY KEY (ID,LastName);
```

`Notă`: Dacă utilizați `ALTER TABLE` pentru a adăuga un `PRIMARY KEY`, coloanele `PRIMARY KEY` trebuie să fi fost declarate ca nu conțin valori `NULL` (când tabelul a fost creat pentru prima dată).

## DROP un PRIMARY KEY Constraint
Pentru a elimina un `PRIMARY KEY Constraint`, utilizați următorul SQL:

### MySQL:

```sql
ALTER TABLE Persons
DROP PRIMARY KEY;
```

### SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Persons
DROP CONSTRAINT PK_Person;
```