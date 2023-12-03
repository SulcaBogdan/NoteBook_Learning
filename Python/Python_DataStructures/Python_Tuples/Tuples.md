# Tuple in Python

### Tuple sunt folosite pentru a stoca mai multe elemente intr-o variabila.

Aceasta este una din cele 4 structuri de date din Python, respectiv **listele**, **dictionarele** si **set-urile**

**Tuple sunt colectii organizate si imutabile (odata initializate nu se mai pot modifica)**

### Tuple se initializeaza intre paranteze rotunde () comparativ cu listele care se noteaza intre paranteze patrare []

Exemplu de tuple:

```python
#Am initializat o variabila cu un tuple cu 4 elemente numerice
my_tuple = (1,2,3,4)

print(my_tuple)

output:
(1,2,3,4)
```

### Tuple permite elemente dublicate

De exemplu:

```python
my_tuple = (1,2,1,2,3)
my_tuple_text = ("Dodan", "Bogdan", "Dodan")

print(my_tuple)
print(my_tuple_text)

output:
(1,2,1,2,3)
("Dodan", "Bogdan", "Dodan")
```

### Pentru aflarea lungimii unei tuple folosim functia len()

```python
my_tuple_text = ("Dodan", "Bogdan", "Dodan")

print(len(my_tuple_text))

output:
3
```

### Daca vrem sa creeam o tupla cu un singur item putem scrie elementul si pune "," dupa

De exemplu:

```python
my_tuple_text = ("Dodan",)

print(my_tuple_text)

output:
(Dodan,)
```

### Tuple pot fi initializate cu toate tipurile de date

De exemplu:

```python
tuple_string = ("Dodan", "Masina")
tuple_int = (1,2,3,4)
tuple_bool = (True, False, True)

#Pot avea tipuri de date amestecate
tuple_mix = ("Dodan", 25, True)
```

### Putem crea o tuple folosind si constructorul tuple()

De exemplu:

```python
my_tuple = tuple((1,2,3,4)) # dubla paranteza

print(my_tuple)

output:
(1,2,3,4)
```

