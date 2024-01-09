# UNION in SQL

Operatorul `UNION` este folosit pentru a combina setul de rezultate din două sau mai multe instrucțiuni `SELECT`.

Fiecare instrucțiune `SELECT` din `UNION` trebuie să aibă același număr de coloane
De asemenea, coloanele trebuie să aibă tipuri de date similare
De asemenea, coloanele din fiecare instrucțiune SELECT trebuie să fie în aceeași ordine


## Sintaxa UNION

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

## Sintaxa UNION ALL
Operatorul `UNION` selectează implicit numai valori distincte. Pentru a permite valori duplicate, utilizați `UNION ALL`:

```sql
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

`Notă`: Numele coloanelor din setul de rezultate sunt de obicei egale cu numele coloanelor din prima instrucțiune `SELECT`.

În acest tutorial vom folosi binecunoscuta bază de date mostre `Northwind`.

Mai jos este o selecție din tabelul `Clients`:

| `CustomerID` | `CustomerName`                      | `ContactName`    | `Address`                          | `City`           | `PostalCode` | `Country` |
|------------|----------------------------------|-----------------|----------------------------------|----------------|------------|---------|
| 1          | Alfreds Futterkiste              | Maria Anders    | Obere Str. 57                    | Berlin         | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados| Ana Trujillo    | Avda. de la Constitución 2222    | México D.F.    | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería          | Antonio Moreno  | Mataderos 2312                   | México D.F.    | 05023      | Mexico  |


Și o selecție din tabelul `Suppliers`:

| `SupplierID` | `SupplierName`                   | `ContactName`     | `Address`                  | `City`         | `PostalCode` | `Country` |
|------------|---------------------------------|------------------|--------------------------|--------------|------------|---------|
| 1          | Exotic Liquid                   | Charlotte Cooper | 49 Gilbert St.           | London       | EC1 4SD    | UK      |
| 2          | New Orleans Cajun Delights      | Shelley Burke    | P.O. Box 78934           | New Orleans  | 70117      | USA     |
| 3          | Grandma Kelly's Homestead       | Regina Murphy    | 707 Oxford Rd.           | Ann Arbor    | 48104      | USA     |


### Exemplu SQL UNION
Următoarea instrucțiune SQL returnează orașele (doar valori distincte) atât din tabelul `Clients`, cât și din tabelul `Suppliers`.

```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;
```

`Notă`: Dacă unii **clienți** sau **furnizori** au același oraș, fiecare oraș va fi listat o singură dată, deoarece `UNION` selectează doar valori distincte. Utilizați `UNION ALL` pentru a selecta și valori duplicate!

## Exemplu SQL UNION ALL 
Următoarea instrucțiune SQL returnează orașele (de asemenea, valorile duplicate) din tabelul `Clients` și `Suppliers`:

```sql
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
```

## SQL UNION Cu WHERE
Următoarea instrucțiune SQL returnează orașele germane (doar valori distincte) atât din tabelul `Clients`, cât și din tabelul `Suppliers`:

```sql
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;
```

## SQL UNION ALL Cu WHERE
Următoarea instrucțiune SQL returnează orașele germane (de asemenea, valori duplicate) din tabelul `Clients` și `Suppliers`:

```sql
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION ALL
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;
```

### Un alt exemplu de UNION
Următoarea instrucțiune SQL listează toți **clienții** și **furnizorii**:

```sql
SELECT 'Customer' AS Type, ContactName, City, Country
FROM Customers
UNION
SELECT 'Supplier', ContactName, City, Country
FROM Suppliers;
```