# SQL VALORILE NULL

## Ce este o Valoare NULL?
Un câmp cu o valoare `NULL` este un câmp fără valoare.

Dacă un câmp dintr-un tabel este opțional, este posibil să inserăm o înregistrare nouă sau să actualizăm o înregistrare fără a adăuga o valoare în acest câmp. În acest caz, câmpul va fi salvat cu o valoare `NULL`.

**Notă**: O valoare `NULL` este diferită de o valoare `zero` sau de un câmp care conține spații. Un câmp cu o valoare `NULL` este unul care a fost lăsat gol în timpul creării înregistrării!


## Cum Testăm pentru Valori NULL?
Nu este posibil să testăm valorile NULL cu operatori de comparație, cum ar fi =, < sau <>.

Va trebui să folosim operatorii IS NULL și IS NOT NULL în schimb.

## Sintaxa IS NULL

```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```

## Sintaxa IS NOT NULL

```sql
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```

## Exemplu pentru Valori NULL
| CustomerID | CustomerName                   | ContactName      | Address                         | City       | PostalCode | Country  |
|------------|--------------------------------|------------------|---------------------------------|------------|------------|----------|
| 1          | Alfreds Futterkiste            | Maria Anders     | Obere Str. 57                   | Berlin     | 12209      | Germany  |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo  | Avda. de la Constitución 2222  | México D.F. | 05021      | Mexico   |
| 3          | Antonio Moreno Taquería        | Antonio Moreno   | Mataderos 2312                  | México D.F. | 05023      | Mexico   |
| 4          | Around the Horn                 | Thomas Hardy     | 120 Hanover Sq.                 | London     | WA1 1DP    | UK       |
| 5          | Berglunds snabbköp              | Christina Berglund | Berguvsvägen 8               | Luleå      | S-958 22   | Sweden   |

## Operatorul IS NULL
Operatorul `IS NULL` este folosit pentru a testa pentru valori goale (valori `NULL`).

Următoarea instrucțiune SQL listează toți clienții cu o valoare `NULL` în câmpul "`Address`":

```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```

### Sfat: Folosește întotdeauna `IS NULL` pentru a căuta valori `NULL`.

## Operatorul IS NOT NULL
Operatorul `IS NOT NULL` este folosit pentru a testa pentru valori negoale (valori `NOT NULL`).

Următoarea instrucțiune SQL listează toți clienții cu o valoare în câmpul "`Address`":
```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```


