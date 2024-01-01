# ALIASES in SQL

Operatori de `Alias` în SQL

Operatorii de `alias` în SQL sunt utilizați pentru a oferi unei tabele sau unei coloane dintr-o tabel, un nume temporar.

Aliasurile sunt adesea folosite pentru a face numele coloanelor mai ușor de citit.

- Un alias există doar pe durata acelei interogări.

- Un alias este creat cu ajutorul cuvântului cheie AS.

Exemplu

```sql
SELECT CustomerID AS ID
FROM Customers;
```

## AS este opțional

De fapt, în majoritatea limbajelor de bază de date, poți sări peste cuvântul cheie `AS` și să obții același rezultat:

Exemplu

```sql
SELECT CustomerID ID
FROM Customers;
```
## Sintaxă

Când aliasul este folosit pe o coloană:

```sql
SELECT column_name AS alias_name
FROM table_name;
```
Când aliasul este folosit pe o tabelă:
```sql
SELECT column_name(s)
FROM table_name AS alias_name;
```

### Bază de date demonstrativă

Mai jos este o selecție din tabelele Customers și Orders utilizate în exemple:

### Tabela Customers

| CustomerID | CustomerName                     | ContactName      | Address                  | City         | PostalCode | Country |
|------------|----------------------------------|------------------|--------------------------|--------------|------------|---------|
| 1          | Alfreds Futterkiste              | Maria Anders     | Obere Str. 57            | Berlin       | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F.  | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería          | Antonio Moreno   | Mataderos 2312           | México D.F.  | 05023      | Mexico  |

### Tabela Orders

| OrderID | CustomerID | EmployeeID | OrderDate  | ShipperID |
|---------|------------|------------|------------|-----------|
| 10248   | 90         | 5          | 7/4/1996   | 3         |
| 10249   | 81         | 6          | 7/5/1996   | 1         |
| 10250   | 34         | 4          | 7/8/1996   | 2         |


## Aliasuri pentru Coloane

Următoarea instrucțiune SQL creează două aliasuri, unul pentru coloana `CustomerID` și unul pentru coloana CustomerName:

Exemplu

```sql
SELECT CustomerID AS ID, CustomerName AS Customer
FROM Customers;
```
## Utilizarea Aliasurilor cu un Caracter Spațiu

Dacă dorești ca aliasul să conțină unul sau mai multe spații, cum ar fi "My Great Products", înconjoară aliasul cu paranteze pătrate sau ghilimele duble.

Exemplu

Folosirea parantezelor pătrate pentru aliasuri cu caractere spațiu:

```sql
SELECT ProductName AS [My Great Products]
FROM Products;
```
Exemplu

Folosirea ghilimelelor duble pentru aliasuri cu caractere spațiu:

```sql
SELECT ProductName AS "My Great Products"
FROM Products;
```

**Notă**: Unele sisteme de baze de date permit atât `[]` cât și `""`, iar altele permit doar unul dintre ele.

## Concatenarea Coloanelor

Următoarea instrucțiune SQL creează un alias numit "`Address`" care combină patru coloane (`Address`, `PostalCode`, `City` și `Country`):

### Exemplu

```sql
SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
FROM Customers;
```

**Notă**: Pentru a face ca instrucțiunea SQL de mai sus să funcționeze în MySQL, utilizează următoarea formulare:

### Exemplu MySQL

```sql
SELECT CustomerName, CONCAT(Address,', ',PostalCode,', ',City,', ',Country) AS Address
FROM Customers;
```

**Notă**: Pentru a face ca instrucțiunea SQL de mai sus să funcționeze în Oracle, utilizează următoarea formă:

 ### Exemplu Oracle


 ```sql
 SELECT CustomerName, (Address || ', ' || PostalCode || ' ' || City || ', ' || Country) AS Address
FROM Customers;
```

## Aliasuri pentru Tabele

Aceleași reguli se aplică atunci când dorești să folosești un alias pentru o tabelă.

Exemplu

Fă referire la tabela Customers ca Persons:

```sql
SELECT * FROM Customers AS Persons;
```

S-ar putea să pară inutil să folosești aliasuri pentru tabele, dar atunci când folosești mai mult de o tabelă în interogările tale, poate face declarațiile SQL mai scurte.

Următoarea instrucțiune SQL selectează toate comenzile de la clientul cu CustomerID=4 (Around the Horn). Folosim tabelele "Customers" și "Orders", și le dăm aliasurile de "c" și "o" respectiv (Aici folosim aliasuri pentru a face SQL-ul mai scurt):

```sql
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;
```

Următoarea instrucțiune SQL este aceeași ca cea de mai sus, dar fără aliasuri:

Exemplu

```sql
SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName
FROM Customers, Orders
WHERE Customers.CustomerName='Around the Horn' AND Customers.CustomerID=Orders.CustomerID;
```

Aliasurile pot fi utile atunci când:

- Sunt implicate mai mult de o tabelă într-o interogare
- Sunt utilizate funcții în interogare
- Numele coloanelor sunt lungi sau dificil de citit
- Două sau mai multe coloane sunt combinate



