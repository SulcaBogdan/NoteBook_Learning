# Operatorul LIKE SQL


Operatorul `LIKE` este folosit într-o clauză `WHERE` pentru a căuta un model specificat într-o coloană.

Există două metacaractere folosite adesea împreună cu operatorul `LIKE`:

  - Semnul procentual `%` reprezintă zero, unul sau mai multe caractere
  - Semnul de subliniere `_` reprezintă un singur caracter

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
```

## Sintaxa

```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```


| `CustomerID` | `CustomerName`                 | `ContactName`       | `Address`                    | `City`         | `PostalCode` | `Country` |
|------------|------------------------------|-------------------|----------------------------|--------------|------------|---------|
| 1          | Alfreds Futterkiste          | Maria Anders      | Obere Str. 57              | Berlin       | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo  | Avda. de la Constitución 2222 | México D.F.  | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería      | Antonio Moreno    | Mataderos 2312             | México D.F.  | 05023      | Mexico  |
| 4          | Around the Horn               | Thomas Hardy      | 120 Hanover Sq.            | London       | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp           | Christina Berglund | Berguvsvägen 8           | Luleå        | S-958 22   | Sweden  |




## `_` Wildcard

Caracterul `_` reprezintă un singur caracter. Poate fi orice caracter sau număr, dar fiecare `_` reprezintă un singur caracter.

```sql
SELECT * FROM Customers
WHERE city LIKE 'L_nd__';
```
Returnează toți clienții dintr-un oraș care începe cu „`L`” urmat de un caracter metacar, apoi „`nd`” și apoi două caractere metacara:


## Caracterul wildcard `%`
Caracterul joker `%` reprezintă orice număr de caractere, chiar și zero caractere.

```sql
SELECT * FROM Customers
WHERE city LIKE '%L%';
```

## Incepe cu
Pentru a returna înregistrările care încep cu o anumită literă sau expresie, adăugați `%` la sfârșitul literei sau frazei.

Returnează toți clienții care încep cu „`La`”:
```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'La%';
```
**Nota**: De asemenea, puteți combina orice număr de condiții folosind operatori `AND` sau `OR`.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%' OR CustomerName LIKE 'b%';
```
## Se termină cu
Pentru a returna înregistrările care se termină cu o anumită literă sau expresie, adăugați` %` la începutul literei sau frazei.


Returnează toți clienții care se termină cu „`a`”:
```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%a';
```

**Nota**: De asemenea, puteți combina „`începe cu`” și „`se termină cu`”:

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'b%s';
```

## Conține
Pentru a returna înregistrări care conțin o anumită literă sau expresie, adăugați `% `atât înainte, cât și după literă sau expresie.


Returnează toți clienții care conțin expresia `„sau”`
```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';
```

## Combinați wildcards
Orice wildcard, cum ar fi `%` și `_` , poate fi folosit în combinație cu alte wildcards.


Returnați toți clienții care încep cu „`a`” și au cel puțin 3 caractere:
```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';
```
Returnează toți clienții care au „`r`” în a doua poziție:
```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';
```


## Fără wildcard
Dacă nu este specificat nici un wildcard, expresia trebuie să aibă o potrivire exactă pentru a returna un rezultat.

Returnează toți clienții din Spania:
```sql
SELECT * FROM Customers
WHERE Country LIKE 'Spain';
```

