# For loop

Un for loop este folosit pentru iterarea unei secvențe (adică fie o listă, un tuplu, un dicționar, un set sau un șir).

Acesta seamănă mai puțin cu cuvântul cheie for din alte limbaje de programare și funcționează mai mult ca o metodă iteratoare așa cum se găsește în alte limbaje de programare orientate pe obiecte.

Cu for loop putem executa un set de instrucțiuni, o dată pentru fiecare element dintr-o listă, tuplu, set etc.

```python
fructe = ["mar", "banana", "cirese"]
for x in fructe:
  print(x)

output:
mar
banana
cirese
```

#### Bucla for nu necesită o variabilă de indexare care să fie setată în prealabil.

## Loop printr-un String

Chiar și șirurile sunt obiecte iterabile, ele conțin o secvență de caractere:

```python
for x in "banana":
  print(x)

output:
b
a
n
a
n
a
```

## break statement

Cu instrucțiunea break putem opri bucla înainte ca aceasta să fi parcurs toate elementele:

```python
fructe = ["mar", "banana", "cirese"]
for x in fructe:
  print(x)
  if x == "banana":
    break

output:
mar
banana
```

Ieșiți din loop când x == „banană”, dar de data aceasta break vine înainte de imprimare:

```python
fructe = ["mar", "banana", "cirese"]
for x in fructe:
  if x == "banana":
    break
  print(x)  

output:
mar
```

## continue statement

Cu instrucțiunea continue putem opri iterația curentă a loop-ului și putem continua cu următoarea:

```python
fructe = ["mar", "banana", "cirese"]
for x in fructe:
  if x == "banana":
    continue
  print(x)

output:
mar
cirese
```

## range() function

Pentru a parcurge un cod de un anumit număr de ori, putem folosi funcția **range**(),

Funcția **range**() returnează o secvență de numere, începând de la 0 în mod implicit și crește cu 1 (în mod implicit) și se termină la un număr specificat.

```python
for x in range(6):
  print(x)

output:
0
1
2
3
4
5
```
Funcția range() este implicit 0 ca valoare de pornire, totuși este posibil să specificați valoarea de pornire adăugând un parametru: range(2, 6), ceea ce înseamnă valori de la 2 la 6 (dar fără să includă 6):

```python
for x in range(2, 6):
  print(x)

output:
2
3
4
5
```

Funcția range() în mod implicit crește secvența cu 1, totuși este posibil să specificați valoarea de increment adăugând un al treilea parametru: range(2, 30, 3):

```python
for x in range(2, 30, 3):
  print(x)

output:
2
5
8
11
14
17
20
23
26
29
```

## Else in For Loop

Cuvântul cheie **else** dintr-o buclă for specifică un bloc de cod care trebuie executat când bucla este terminată:

```python
for x in range(6):
  print(x)
else:
  print("Am terminat!")

output:
0
1
2
3
4
5
Am terminat!
```

**Notă: Blocul else NU va fi executat dacă bucla este oprită de o instrucțiune break.**

Break the loop when x is 3, and see what happens with the else block:

```python
for x in range(6):
  if x == 3: break
  print(x)
else:
  print("Finally finished!")

output:
0
1
2
```

## Nested Loops

Un nested loop este un loop în interiorul unui alt loop.

„Inner loop” va fi executată o dată pentru fiecare iterație a "outer loop":

```python
adj = ["red", "big", "tasty"]
fruits = ["apple", "banana", "cherry"]

for x in adj:
  for y in fruits:
    print(x, y)

outout:
red apple
red banana
red cherry
big apple
big banana
big cherry
tasty apple
tasty banana
tasty cherry
```

# pass statement

For loops nu pot fi goale, dar dacă dintr-un motiv oarecare aveți o buclă for fără conținut, introduceți declarația de trecere pentru a evita o eroare.

```python
for x in [0, 1, 2]:
  pass

# avand un for loop ca acesta ar fi ridicat o eroare daca nu aveam pass statement.
```

