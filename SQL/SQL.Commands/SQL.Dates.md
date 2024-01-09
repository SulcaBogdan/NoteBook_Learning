# Lucrul cu date in SQL

Cea mai dificilă parte atunci când lucrați cu date este să vă asigurați că formatul datei pe care încercați să o introduceți se potrivește cu formatul coloanei date din baza de date.

Atâta timp cât datele dvs. conțin doar porțiunea dată, interogările dvs. vor funcționa conform așteptărilor. Cu toate acestea, dacă este implicată o porțiune de timp, devine mai complicat.

Iată tipurile de date pentru stocarea datelor și valorilor date/timp în MySQL și SQL Server, împreună cu formatele lor:

### MySQL

1. **`DATE`** - format: YYYY-MM-DD
2. **`DATETIME`** - format: YYYY-MM-DD HH:MI:SS
3. **`TIMESTAMP`** - format: YYYY-MM-DD HH:MI:SS
4. **`YEAR`** - format: YYYY sau YY

### SQL Server

1. **`DATE`** - format: YYYY-MM-DD
2. **`DATETIME`** - format: YYYY-MM-DD HH:MI:SS
3. **`SMALLDATETIME`** - format: YYYY-MM-DD HH:MI:SS
4. **`TIMESTAMP`** - format: un număr unic

`Notă`: Tipurile de date pentru dată sunt selectate pentru o coloană atunci când creezi o nouă tabelă în baza ta de date!

## Exemplu

### Tabelul Orders 

| `OrderId` | `ProductName`           | `OrderDate`  |
|---------|-----------------------|------------|
| 1       | Geitost               | 2008-11-11 |
| 2       | Camembert Pierrot     | 2008-11-09 |
| 3       | Mozzarella di Giovanni| 2008-11-11 |
| 4       | Mascarpone Fabioli    | 2008-10-29 |

Acum dorim să selectăm înregistrările cu data de comandă „2008-11-11” din tabelul de mai sus.

Folosim următoarea instrucțiune `SELECT`:


```SELECT * FROM Orders WHERE OrderDate='2008-11-11'```


Setul de rezultate va arăta astfel:

| `OrderId` | `ProductName`           | `OrderDate`  |
|---------|-----------------------|------------|
| 1       | Geitost               | 2008-11-11 |
| 3       | Mozzarella di Giovanni| 2008-11-11 |


`Notă`: **Două date pot fi comparate cu ușurință dacă nu este implicată nicio componentă de timp!**

Acum, să presupunem că tabelul `Orders` arată astfel (observați componenta de timp adăugată în coloana `OrderDate`):

| `OrderId` | `ProductName`           | `OrderDate`            |
|---------|-----------------------|----------------------|
| 1       | Geitost               | 2008-11-11 13:23:44  |
| 2       | Camembert Pierrot     | 2008-11-09 15:45:21  |
| 3       | Mozzarella di Giovanni| 2008-11-11 11:12:01  |
| 4       | Mascarpone Fabioli    | 2008-10-29 14:56:59  |


Dacă folosim aceeași instrucțiune `SELECT` ca mai sus:

```sql SELECT * FROM Orders WHERE OrderDate='2008-11-11'```

Nu vom obține niciun rezultat! Acest lucru se datorează faptului că interogarea caută numai date fără porțiune de timp.

`Note`: Pentru a vă menține interogările simple și ușor de întreținut, nu utilizați componente de timp în datele dvs., decât dacă este necesar!

