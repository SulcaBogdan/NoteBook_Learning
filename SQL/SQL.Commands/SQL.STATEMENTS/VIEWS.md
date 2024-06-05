# VIEWS in SQL

În SQL, un `VIEW` este un tabel virtual bazat pe setul de rezultate al unei instrucțiuni SQL.

Un VIEW conține **rânduri** și **coloane**, la fel ca un tabel real. Câmpurile dintr-un VIEW sunt câmpuri dintr-unul sau mai multe tabele reale din baza de date.

Puteți adăuga `VIEWS` și funcții SQL la o vizualizare și puteți prezenta datele ca și cum datele ar proveni dintr-un singur tabel.

Un `VIEW` este creată cu instrucțiunea `CREATE VIEW`.

## Sintaxa

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

`Notă`: Un `VIEW` arată întotdeauna date actualizate! Motorul bazei de date recreează VIEW-UL, de fiecare dată când un utilizator o interoghează.

## Exemplu CREATE VIEW

Următorul SQL creează un `VIEW` care arată toți clienții din Brazilia:

```sql
CREATE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil';
```


Putem interoga VIEW-ul de mai sus după cum urmează:

```sql
SELECT * FROM [Brazil Customers];
```

Următorul cod SQL creează un `VIEW` care selectează fiecare produs din tabelul `Products` cu un preț mai mare decât prețul mediu:

```sql
CREATE VIEW [Products Above Average Price] AS
SELECT ProductName, Price
FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);
```
Putem interoga VIEW-ul de mai sus după cum urmează:

```sql
SELECT * FROM [Products Above Average Price];
```

## SQL Updating a View

O vizualizare poate fi actualizată cu instrucțiunea `CREATE OR REPLACE VIEW`.

## SQL CREATE OR REPLACE VIEW Sintaxă

```SQL
CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
Următorul SQL adaugă coloana `City` la vizualizarea `Brazil Customers`:

```sql
CREATE OR REPLACE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName, City
FROM Customers
WHERE Country = 'Brazil';
```

## SQL Dropping a View

Un `VIEW` este ștearsă cu instrucțiunea `DROP VIEW`.

## Sintaxa

```sql
DROP VIEW view_name;
```

Următorul SQL elimină VIEW-ul `Brazil Customers`:

```sql
DROP VIEW [Brazil Customers];
```




