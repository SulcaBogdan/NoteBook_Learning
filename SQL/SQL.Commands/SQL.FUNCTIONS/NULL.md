# Functiile NULL in SQL

Funcții SQL `IFNULL()`, `ISNULL()`, `COALESCE()` și `NVL()`
Consultați următorul tabel `Products`:

| `P_Id` | `ProductName` | `UnitPrice` | `UnitsInStock` | `UnitsOnOrder` |
|------|-------------|-----------|--------------|--------------|
| 1    | Jarlsberg   | 10.45     | 16           | 15           |
| 2    | Mascarpone  | 32.56     | 23           |              |
| 3    | Gorgonzola  | 15.67     | 9            | 20           |


Să presupunem că coloana `„UnitsOnOrder”` este opțională și poate conține valori `NULL`.

Priviți următoarea instrucțiune `SELECT`:

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + UnitsOnOrder)
FROM Products;
```

În exemplul de mai sus, dacă oricare dintre valorile `„UnitsOnOrder”` este `NULL`, rezultatul va fi `NULL`.

## Soluții

Funcția MySQL `IFNULL()` vă permite să returnați o valoare alternativă dacă o expresie este `NULL`:

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))
FROM Products;
```

sau putem folosi funcția `COALESCE()`, astfel:

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;
```

#### SQL Server

Funcția SQL Server `ISNULL()` vă permite să returnați o valoare alternativă atunci când o expresie este `NULL`:

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0))
FROM Products;
```

sau putem folosi funcția `COALESCE()`, astfel:

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;
```

#### MS Access

Funcția MS Access IsNull() returnează TRUE (-1) dacă expresia este o valoare nulă, în caz contrar FALSE (0):

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + IIF(IsNull(UnitsOnOrder), 0, UnitsOnOrder))
FROM Products;
```

#### Oracle

Funcția Oracle `NVL()` obține același rezultat:

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + NVL(UnitsOnOrder, 0))
FROM Products;
```

sau putem folosi funcția `COALESCE()`, astfel:

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;
```