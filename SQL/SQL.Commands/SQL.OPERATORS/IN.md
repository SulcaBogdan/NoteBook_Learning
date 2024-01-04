# Operatorul IN SQL


Operatorul `IN` îți permite să specifici mai multe valori într-o clauză `WHERE`.

Operatorul `IN` este o prescurtare pentru mai multe condiții OR.

### Exemplu
Întoarce toți clienții din 'Germania', 'Franța' sau 'Marea Britanie'

```sql
SELECT * FROM Customers
WHERE Country IN ('Germania', 'Franța', 'Marea Britanie');
```

## Sintaxă
```sql
SELECT nume_coloană(e)
FROM nume_tabel
WHERE nume_coloană IN (valoare1, valoare2, ...);
```

### Bază de date demonstrativă
Mai jos este o selecție din tabela `Customers` folosită în exemple:

`CustomerID` | `CustomerName` | `ContactName` | `Address` | `City` | `PostalCode` | `Country`
---|---|---|---|---|---|---
1 | Alfreds Futterkiste | Maria Anders | Obere Str. 57 | Berlin | 12209 | Germania
2 | Ana Trujillo Emparedados y helados | Ana Trujillo | Avda. de la Constitución 2222 | México D.F. | 05021 | Mexic
3 | Antonio Moreno Taquería | Antonio Moreno | Mataderos 2312 | México D.F. | 05023 | Mexic
4 | Around the Horn | Thomas Hardy | 120 Hanover Sq. | Londra | WA1 1DP | Marea Britanie
5 | Berglunds snabbköp | Christina Berglund | Berguvsvägen 8 | Luleå | S-958 22 | Suedia

## NOT IN
Prin utilizarea cuvântului cheie `NOT` în fața operatorului `IN`, vei returna toate înregistrările care NU sunt niciuna dintre valorile din listă.

### Exemplu
Întoarce toți clienții care NU sunt din '`Germania`', '`Franța`' sau '`Marea Britanie`':

```sql
SELECT * FROM Customers
WHERE Country NOT IN ('Germania', 'Franța', 'Marea Britanie');
```

## IN (SELECT)
Poți folosi, de asemenea, `IN` cu o subinterogare în clauza `WHERE`.

Cu o subinterogare, poți returna toate înregistrările din interogarea principală care sunt prezente în rezultatul subinterogării.

### Exemplu
Întoarce toți clienții care au o comandă în tabela Orders:

```sql
SELECT * FROM Customers
WHERE CustomerID IN (SELECT CustomerID FROM Orders);
```

## NOT IN (SELECT)
Rezultatul din exemplul de mai sus a întors 74 de înregistrări, ceea ce înseamnă că există 17 clienți care nu au plasat nicio comandă.

Să verificăm dacă este corect, prin utilizarea operatorului `NOT IN`.

### Exemplu
Întoarce toți clienții care `NU` au plasat nicio comandă în tabela `Orders`:

```sql
SELECT * FROM Customers
WHERE CustomerID NOT IN (SELECT CustomerID FROM Orders);
```
