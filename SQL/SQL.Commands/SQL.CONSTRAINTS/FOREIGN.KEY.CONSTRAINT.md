# SQL FOREIGN KEY Constraint

`FOREIGN KEY Constraint` este utilizată pentru a preveni acțiunile care ar distruge legăturile dintre tabele.

O `FOREIGN KEY` este un câmp (sau o colecție de câmpuri) dintr-un tabel, care se referă la `PRIMARY KEY` dintr-un alt tabel.

Tabelul cu `FOREIGN KEY` se numește tabel copil, iar tabelul cu `PRIMARY KEY` se numește tabelul referit sau părinte.

Priviți următoarele două tabele:

### Tabelul Persons

| `PersonID` | `LastName`  | `FirstName` | `Age` |
|----------|-----------|-----------|-----|
| 1        | Hansen    | Ola       | 30  |
| 2        | Svendson  | Tove      | 23  |
| 3        | Pettersen | Kari      | 20  |


### Tabelul Orders

| `OrderID` | `OrderNumber` | `PersonID` |
|---------|-------------|----------|
| 1       | 77895       | 3        |
| 2       | 44678       | 3        |
| 3       | 22456       | 2        |
| 4       | 24562       | 1        |


Observați că coloana `PersonID` din tabelul `Orders` indică coloana `PersonID` din tabelul `Persons`.

Coloana `PersonID` din tabelul `Persons` este `PRIMARY KEY` din tabelul `Persons`.

Coloana `PersonID` din tabelul `Orders` este o `FOREIGN KEY` în tabelul `Orders`.

`FOREIGN KEY Constraint` împiedică inserarea datelor invalide în coloana cheii externe, deoarece trebuie să fie una dintre valorile conținute în tabelul părinte.

## SQL FOREIGN KEY on CREATE TABLE

Următorul SQL creează o `FOREIGN KEY` pe coloana `„PersonID”` atunci când este creat tabelul `Orders`:

### MySQL:

```sql
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
```

### SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Orders (
    OrderID int NOT NULL PRIMARY KEY,
    OrderNumber int NOT NULL,
    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
);
```

Pentru a permite denumirea unui `FOREIGN KEY Constraint` și pentru a defini un `FOREIGN KEY Constraint` pe mai multe coloane, utilizați următoarea sintaxă SQL:


### MySQL / SQL Server / Oracle / MS Access:

```sql
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);
```

## SQL FOREIGN KEY on ALTER TABLE

Pentru a crea un `FOREIGN KEY Constraint` pe coloana `„PersonID”` când tabelul `Orders` este deja creat, utilizați următorul SQL:

### MySQL / SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Orders
ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```

Pentru a permite denumirea unui `FOREIGN KEY Constraint` și pentru a defini un `FOREIGN KEY Constraint` pe mai multe coloane, utilizați următoarea sintaxă SQL:

### MySQL / SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```
## DROP a FOREIGN KEY Constraint
Pentru a elimina un `FOREIGN KEY Constraint`, utilizați următorul SQL:

### MySQL:

```sql
ALTER TABLE Orders
DROP FOREIGN KEY FK_PersonOrder;
```

### SQL Server / Oracle / MS Access:

```sql
ALTER TABLE Orders
DROP CONSTRAINT FK_PersonOrder;
```

