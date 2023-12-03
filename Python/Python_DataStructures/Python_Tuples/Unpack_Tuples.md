# Unpack Tuples

### De obicei cand declaram un tuple il si initializam cu niste valori. Acest procedeu se numeste **"packing"** sau boxing

De exemplu:

```python
my_tuple = (1,2,3,4)

print(my_tuple)

output:
(1,2,3,4)
```

### In Python ni se permite sa extragem valorile inapoi in variabile . Acest procedeu se numeste "unpacking" sau unboxing

```python
my_tuple = ("Dodan", "Bogdan", "Marius", "Alina")
# Am atribuit fiecarei variabile nume1, nume2 etc o valoare din tupla noastra 
# dupa index. adica nume1 = index 0 my_tuple, nume2 = index 1 my_tuple etc..
(nume1, nume2, nume3, nume4) = my_tuple

print(nume1)
print(nume2)
print(nume3)
print(nume4)

output:
Dodan
Bogdan
Marius
Alina
```

### Utilizarea '*'

Daca tuplul nostru are mai multe elemente decat variabilele noastre putem folosii '*' pentru a atribui ultimei variabile restul elementelor din tuple.

```python
fructe = ("mar", "banana", "cirese", "capsuna", "zmeura")

(verde, galben, *rosu) = fruits

print(verde)
print(galben)
print(rosu)

output:
mar
banana
("cirese", "capsuna", "zmeura")
```

Daca '*' este adaugata inaintea ultimei variabile atunci i se vor atribuii acelei variabile toate elementele pana in ultima variabila.

```python
fructe = ("mar", "banana", "cirese", "capsuna", "zmeura")

(verde, *galben, rosu) = fruits

print(verde)
print(galben)
print(rosu)

output:
mar
("banana", "cirese", "capsuna")
zmeura
```

