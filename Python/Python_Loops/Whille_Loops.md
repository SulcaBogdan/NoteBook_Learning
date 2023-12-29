# While loops

Python are doua comenzi de loop primitive

1. for loop
2. while loop

## While loop

Cu while loop putem executa un set de instrucțiuni atâta timp cât o condiție este adevărată.

```python
i = 1
while i < 6:
  print(i)
  i += 1

output:
1
2
3
4
5
```
While loop necesită ca variabilele relevante să fie pregătite, în acest exemplu trebuie să definim o variabilă de indexare, i, pe care o setăm la 1.


## break statement

Cu instrucțiunea break putem opri loop-ul chiar dacă condiția while este adevărată:

```python
i = 1
while i < 6:
  print(i)
  if i == 3:
    break
  i += 1

output:
1
2
3
```

## continue statement

Cu instrucțiunea continue putem opri iterația curentă și continua cu următoarea:

```python
i = 0
while i < 6:
  i += 1
  if i == 3:
    continue
  print(i)

# Atentie numarul 3 nu exista in rezultat deoarece cand i a fost 3 nu s-a
# modificat sau printat nimic ci doar s-a mers mai departe

output:
1
2
4
5
6
```

## else statement

```python
i = 1
while i < 6:
  print(i)
  i += 1
else:
  print("i nu mai este mai mic ca 6")

output:
1
2
3
4
5
i nu mai este mai mic ca 6
```

