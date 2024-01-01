# Caractere Wildcard în SQL
Un caracter wildcard este folosit pentru a înlocui unul sau mai mulți caractere într-un șir.

Caracterele wildcard sunt utilizate împreună cu operatorul `LIKE`. Operatorul `LIKE` este folosit într-o clauză `WHERE` pentru a căuta un model specific într-o coloană.

Exemplu
Returnează toți clienții care încep cu litera 'a':

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
```

# Caractere Wildcard

| Simbol | Descriere                                              |
|--------|--------------------------------------------------------|
| `%`     | Reprezintă zero sau mai multe caractere               |
| `_`      | Reprezintă un singur caracter                          |
| `[]`     | Reprezintă oricare caracter din interiorul parantezelor |
| `^`      | Reprezintă orice caracter care nu este în parantezele pătrate |
| `-`      | Reprezintă oricare caracter în cadrul intervalului specificat |
| `{}`     | Reprezintă orice caracter scăpat                       |

*Notă:*
- *Nu este suportat în bazele de date PostgreSQL și MySQL.*
- *Suportat doar în bazele de date Oracle.*





## Exemplu de Bază de Date
Mai jos este o selecție din tabela `Customers` utilizată în exemple:

# Tabel Customer

| `CustomerID` | `CustomerName`                  | `ContactName`      | `Address`                    | `City`           | `PostalCode` | `Country` |
|------------|-------------------------------|-------------------|----------------------------|----------------|------------|---------|
| 1          | Alfreds Futterkiste           | Maria Anders      | Obere Str. 57               | Berlin          | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo  | Avda. de la Constitución 2222 | México D.F.   | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería       | Antonio Moreno    | Mataderos 2312             | México D.F.   | 05023      | Mexico  |
| 4          | Around the Horn               | Thomas Hardy      | 120 Hanover Sq.            | London         | WA1 1DP    | UK      |
| 5          | Berglunds snabbköp            | Christina Berglund| Berguvsvägen 8            | Luleå          | S-958 22   | Sweden  |


## Utilizarea Caracterului % Wildcard
Caracterul `%` wildcard reprezintă orice număr de caractere, chiar și zero caractere.

Exemplu
- Returnează toți clienții care se termină cu modelul '`es`':

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%es';
```

- Returnează toți clienții care conțin modelul '`mer`':

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%mer%';
```

## Utilizarea Caracterului _ Wildcard
Caracterul `_` wildcard reprezintă un singur caracter.

Poate fi orice caracter sau număr, dar fiecare `_` reprezintă un singur caracter.

Exemplu
- Returnează toți clienții cu un oraș care începe cu orice caracter, urmat de "`ondon`":

```sql
SELECT * FROM Customers
WHERE City LIKE '_ondon';
```

```sql
SELECT * FROM Customers
WHERE City LIKE '_ondon';
```

- Returnează toți clienții cu un oraș care începe cu "**L**", urmat de oricare 3 caractere, terminându-se cu "**on**":

```sql
SELECT * FROM Customers
WHERE City LIKE 'L___on';
```

## Utilizarea Caracterului [] Wildcard
Caracterul `[]` wildcard returnează un rezultat dacă oricare dintre caracterele din interior primesc o potrivire.

Exemplu
Returnează toți clienții care încep cu "`b`", "`s`" sau "`p`":

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '[bsp]%';
```

## Utilizarea Caracterului - Wildcard
Caracterul `-` wildcard vă permite să specificați un interval de caractere în interiorul caracterului `[]` wildcard.

Exemplu
Returnează toți clienții care încep cu "`a`", "`b`", "`c`", "`d`", "`e`" sau "`f`":

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '[a-f]%';
```

## Combinarea Caracterelor Wildcard
Orice caracter wildcard, cum ar fi `%` și `_`, poate fi folosit în combinație cu alte caractere wildcard.

Exemplu
- Returnează toți clienții care încep cu "`a`" și au cel puțin 3 caractere în lungime:

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';
```

- Returnează toți clienții care au "`r`" pe a doua poziție:

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';
```

## Fără Wildcard
Dacă nu este specificat niciun wildcard, expresia trebuie să aibă o potrivire exactă pentru a returna un rezultat.

Exemplu
Returnează toți clienții din Spania:

```sql
SELECT * FROM Customers
WHERE Country LIKE 'Spain';
```

# Caractere Wildcard în Microsoft Access

| Symbol | Description                                      | Example                         |
|--------|--------------------------------------------------|---------------------------------|
| *      | Reprezintă zero sau mai multe caractere         | `bl*` găsește bl, black, blue și blob |
| ?      | Reprezintă un singur caracter                    | `h?t` găsește hot, hat și hit   |
| []     | Reprezintă oricare dintre caracterele din interiorul parantezelor pătrate | `h[oa]t` găsește hot și hat, dar nu hit |
| !      | Reprezintă orice caracter care nu se află în parantezele pătrate | `h[!oa]t` găsește hit, dar nu hot și hat |
| -      | Reprezintă un singur caracter în cadrul intervalului specificat | `c[a-b]t` găsește cat și cbt |
| #      | Reprezintă un singur caracter numeric             | `2#5` găsește 205, 215, 225, 235, 245, 255, 265, 275, 285 și 295 |

