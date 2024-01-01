# JOIN SQL

## JOIN în SQL

O clauză `JOIN` este folosită pentru a combina rânduri din două sau mai multe tabele, bazându-se pe o coloană legată între ele.

Să privim o selecție din tabela "Orders":

| OrderID | CustomerID | OrderDate  |
|---------|------------|------------|
| 10308   | 2          | 1996-09-18 |
| 10309   | 37         | 1996-09-19 |
| 10310   | 77         | 1996-09-20 |


Apoi, să privim o selecție din tabela "Customers":

| CustomerID | CustomerName                       | ContactName    | Country |
|------------|------------------------------------|----------------|---------|
| 1          | Alfreds Futterkiste                | Maria Anders   | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Mexico  |
| 3          | Antonio Moreno Taquería            | Antonio Moreno | Mexico  |


Observă că coloana "`CustomerID`" din tabela "`Orders`" se referă la "`CustomerID`" din tabela "`Customers`". Relația dintre cele două tabele este coloana "`CustomerID`".

Apoi, putem crea următoarea instrucțiune SQL (care conține un INNER JOIN), care selectează înregistrările care au valori potrivite în ambele tabele:

Exemplu

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```

și va produce ceva similar cu:

| OrderID | CustomerName                       | OrderDate  |
|---------|------------------------------------|------------|
| 10308   | Ana Trujillo Emparedados y helados | 9/18/1996  |
| 10365   | Antonio Moreno Taquería            | 11/27/1996 |
| 10383   | Around the Horn                    | 12/16/1996 |
| 10355   | Around the Horn                    | 11/15/1996 |
| 10278   | Berglunds snabbköp                 | 8/12/1996  |


## Diferite Tipuri de JOIN-uri în SQL

Aici sunt diferitele tipuri de JOIN-uri în SQL:

- **(INNER) JOIN**: Returnează înregistrările care au valori potrivite în ambele tabele
- **LEFT (OUTER) JOIN**: Returnează toate înregistrările din tabela stângă și înregistrările potrivite din tabela dreaptă
  
- **RIGHT (OUTER) JOIN**: Returnează toate înregistrările din tabela dreaptă și înregistrările potrivite din tabela stângă
 
- **FULL (OUTER) JOIN**: Returnează toate înregistrările atunci când există o potrivire în oricare dintre tabelele stângă sau dreaptă
 


<div style="display: flex;flex-direction: column; align-items: center;">
  <img src="https://www.w3schools.com/sql/img_inner_join.png" alt="Descrierea imaginii 1">
  <img src="https://www.w3schools.com/sql/img_left_join.png" alt="Descrierea imaginii 2">
  <img src="https://www.w3schools.com/sql/img_right_join.png" alt="Descrierea imaginii 3">
  <img src="https://www.w3schools.com/sql/img_full_outer_join.png" alt="Descrierea imaginii 4">
</div>
