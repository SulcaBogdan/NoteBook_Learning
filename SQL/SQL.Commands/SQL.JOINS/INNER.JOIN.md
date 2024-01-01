# INNER JOIN in SQL

Operatorul `INNER JOIN` selectează înregistrările care au valori potrivite în ambele tabele.

Să ne uităm la o selecție din tabela Products:

| `ProductID` | `ProductName`      | `CategoryID` | `Price` |
|-----------|------------------|------------|-------|
| 1         | Chais            | 1          | 18    |
| 2         | Chang            | 1          | 19    |
| 3         | Aniseed Syrup    | 2          | 10    |

Și o selecție din tabela Categories:

| `CategoryID` | `CategoryName` | `Description`                                        |
|------------|--------------|----------------------------------------------------|
| 1          | Beverages    | Soft drinks, coffees, teas, beers, and ales         |
| 2          | Condiments   | Sweet and savory sauces, relishes, spreads, seasonings |
| 3          | Confections  | Desserts, candies, and sweet breads                 |


Vom uni tabela Products cu tabela `Categories`, folosind câmpul `CategoryID` din ambele tabele:

```sql
SELECT ProductID, ProductName, CategoryName
FROM Products
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

### **Notă**: Operatorul `INNER JOIN` returnează doar rândurile cu o potrivire în ambele tabele. Acest lucru înseamnă că dacă ai un produs fără CategoryID sau cu un CategoryID care nu există în tabela Categories, acea înregistrare nu va fi returnată în rezultat.

## Sintaxa

```sql
SELECT nume_coloană(e)
FROM tabel1
INNER JOIN tabel2
ON tabel1.nume_coloană = tabel2.nume_coloană;
```

## Denumește Coloanele:
Este o practică bună să incluzi numele tabelului atunci când specifici coloanele în instrucțiunea SQL.

Exemplu
Specifică numele tabelului:

```sql
SELECT Products.ProductID, Products.ProductName, Categories.CategoryName
FROM Products
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

Exemplul de mai sus funcționează fără a specifica numele tabelelor, deoarece niciunul dintre numele coloanelor specificate nu este prezent în ambele tabele. Dacă încerci să incluzi CategoryID în instrucțiunea `SELECT`, vei primi o eroare dacă nu specifici numele tabelului (deoarece CategoryID este prezent în ambele tabele).

## JOIN sau INNER JOIN:
`JOIN` și `INNER JOIN` vor returna același rezultat.

`INNER` este tipul implicit de îmbinare pentru `JOIN`, deci atunci când scrii `JOIN`, analizorul de fapt scrie `INNER JOIN`.

Exemplu
`JOIN` este la fel ca `INNER JOIN`:


```sql
SELECT Products.ProductID, Products.ProductName, Categories.CategoryName
FROM Products
JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

## Unirea a Trei Tabele:
Următoarea instrucțiune SQL selectează toate comenzile cu informații despre client și expeditor:

Exemplu

```sql
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);
```


