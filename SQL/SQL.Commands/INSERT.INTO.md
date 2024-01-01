# INSERT INTO SQL


## Instrucțiunea SQL INSERT INTO
Instrucțiunea `INSERT INTO` este folosită pentru a insera înregistrări noi într-o tabelă.

### Sintaxă INSERT INTO
Este posibil să scrii instrucțiunea INSERT INTO în două moduri:

1. Specifică atât numele coloanelor, cât și valorile care trebuie inserate:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

2. Dacă adaugi valori pentru toate coloanele tabelului, nu trebuie să specifici numele coloanelor în interogarea SQL. Cu toate acestea, asigură-te că ordinea valorilor este aceeași cu ordinea coloanelor din tabel. Aici, sintaxa `INSERT INTO` ar fi următoarea:

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

| `CustomerID` | `CustomerName`           | `ContactName`      | `Address`                        | `City`      | `PostalCode` | `Country`  |
|------------|------------------------|------------------|--------------------------------|-----------|------------|----------|
| 89         | White Clover Markets   | Karl Jablonski   | 305 - 14th Ave. S. Suite 3B    | Seattle   | 98128      | USA      |
| 90         | Wilman Kala             | Matti Karttunen  | Keskuskatu 45                  | Helsinki  | 21240      | Finland  |
| 91         | Wolski                  | Zbyszek          | ul. Filtrowa 68                | Walla     | 01-012     | Poland   |


## Exemplu INSERT INTO
Următoarea instrucțiune SQL inserează o înregistrare nouă în tabela "`Customers`":

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```


| `CustomerID` | `CustomerName`           | `ContactName`      | `Address`                        | `City`      | `PostalCode` | `Country`  |
|------------|------------------------|------------------|--------------------------------|-----------|------------|----------|
| 89         | White Clover Markets   | Karl Jablonski   | 305 - 14th Ave. S. Suite 3B    | Seattle   | 98128      | USA      |
| 90         | Wilman Kala             | Matti Karttunen  | Keskuskatu 45                  | Helsinki  | 21240      | Finland  |
| 91         | Wolski                  | Zbyszek          | ul. Filtrowa 68                | Walla     | 01-012     | Poland   |
| 92         | Cardinal                | Tom B. Erichsen  | Skagen 21                      | Stavanger | 4006       | Norway   |


Ai observat că nu am inserat niciun număr în câmpul `CustomerID`?
Coloana `CustomerID` este un câmp de incrementare automată și va fi generată automat atunci când o înregistrare nouă este inserată în tabel.


## Inserare Date Doar în Coloanele Specificate
Este posibil și să inserăm date doar în anumite coloane.

Următoarea instrucțiune SQL va insera o înregistrare nouă, dar va introduce date doar în coloanele "CustomerName", "`City`" și "`Country`" (`CustomerID` va fi actualizat automat):

```sql
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```
| `CustomerID` | `CustomerName`           | `ContactName`      | `Address`                        | `City`      | `PostalCode` | `Country`  |
|------------|------------------------|------------------|--------------------------------|-----------|------------|----------|
| 89         | White Clover Markets   | Karl Jablonski   | 305 - 14th Ave. S. Suite 3B    | Seattle   | 98128      | USA      |
| 90         | Wilman Kala             | Matti Karttunen  | Keskuskatu 45                  | Helsinki  | 21240      | Finland  |
| 91         | Wolski                  | Zbyszek          | ul. Filtrowa 68                | Walla     | 01-012     | Poland   |
| 92         | Cardinal                | null             | null                           | Stavanger | null       | Norway   |


## Inserare Rânduri Multiple
Este posibil și să inserăm mai multe rânduri într-o singură instrucțiune.

Pentru a insera mai multe rânduri de date, folosim aceeași instrucțiune `INSERT INTO`, dar cu mai multe valori:

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES
('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway'),
('Greasy Burger', 'Per Olsen', 'Gateveien 15', 'Sandnes', '4306', 'Norway'),
('Tasty Tee', 'Finn Egan', 'Streetroad 19B', 'Liverpool', 'L1 0AA', 'UK');
```
Asigură-te că separi fiecare set de valori cu o virgulă ,.

Selecția din tabela "`Customers`" va arăta acum așa:

| `CustomerID` | `CustomerName`           | `ContactName`      | `Address`                | `City`       | `PostalCode` | `Country`  |
|------------|------------------------|------------------|------------------------|------------|------------|----------|
| 89         | White Clover Markets   | Karl Jablonski   | 305 - 14th Ave. S. Suite 3B | Seattle   | 98128      | USA      |
| 90         | Wilman Kala             | Matti Karttunen  | Keskuskatu 45          | Helsinki  | 21240      | Finland  |
| 91         | Wolski                  | Zbyszek          | ul. Filtrowa 68        | Walla     | 01-012     | Poland   |
| 92         | Cardinal                | Tom B. Erichsen  | Skagen 21              | Stavanger | 4006       | Norway   |
| 93         | Greasy Burger           | Per Olsen        | Gateveien 15           | Sandnes   | 4306       | Norway   |
| 94         | Tasty Tee               | Finn Egan        | Streetroad 19B         | Liverpool | L1 0AA     | UK       |



