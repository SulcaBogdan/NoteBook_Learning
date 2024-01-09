# SELECT INTO in SQL

Instrucțiunea `SELECT INTO` copiază datele dintr-un tabel într-un tabel nou.

## Sintaxă SELECT INTO 
Copiați toate coloanele într-un tabel nou:

```sql
SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```

Copiați doar câteva coloane într-un tabel nou:

```sql
SELECT column1, column2, column3, ...
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```
Noul tabel va fi creat cu numele și tipurile de coloane așa cum sunt definite în tabelul vechi. Puteți crea nume de coloane noi folosind clauza `AS`.

## Exemplu SELECT INTO

Următoarea instrucțiune SQL creează o copie de rezervă a `Customers`:


```sql
SELECT * INTO CustomersBackup2017
FROM Customers;
```

Următoarea instrucțiune SQL utilizează clauza `IN` pentru a copia tabelul într-un nou tabel dintr-o altă bază de date:

```sql
SELECT * INTO CustomersBackup2017 IN 'Backup.mdb'
FROM Customers;
```

Următoarea instrucțiune SQL copie doar câteva coloane într-un tabel nou:

```sql
SELECT CustomerName, ContactName INTO CustomersBackup2017
FROM Customers;
```

Următoarea instrucțiune SQL copiază doar clienții germani într-un tabel nou:

```sql
SELECT * INTO CustomersGermany
FROM Customers
WHERE Country = 'Germany';
```

Următoarea instrucțiune SQL copie datele din mai mult de un tabel într-un tabel nou:


```sql
SELECT Customers.CustomerName, Orders.OrderID
INTO CustomersOrderBackup2017
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

`Nota`: **`SELECT INTO` poate fi folosit și pentru a crea un tabel nou, gol, folosind schema altuia. Doar adăugați o clauză `WHERE` care face ca interogarea să nu returneze date:**

```sql
SELECT * INTO newtable
FROM oldtable
WHERE 1 = 0;
```
