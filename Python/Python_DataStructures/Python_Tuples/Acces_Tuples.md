# Accesarea Elementelor din Tuple

### Putem accesa elementele din Tuple exact ca in exemplele listelor dupa index sau dupa element.

De exemplu:

```python

thistuple = ("mar", "banana", "cirese")

print(thistuple[1])

output:
banana
```

**Numaratoarea incepe mereu de la 0.**

### Putem accesa si dupa indexul negativ.

De exemplu:

```python
thistuple = ("mar", "banana", "cirese")

print(thistuple[-1])

output:
cirese
```

**Numaratoarea inversa a indexilor incepe mereu de la -1.**

### Putem folosi un concept asemanator cu String Slicing ([start:end:pace]) si pentru tuple.

De exemplu:

```python
thistuple = ("mar", "banana", "cirese", "portocala", "kiwi", "pepene", "mango")

print(thistuple[2:5])

output:
(cirese, portocala, kiwi)
```

### Putem selecta si un interval sau sa inversam la fel prin accesarea indexului negativ.

De exemplu

```python
thistuple = ("mar", "banana", "cirese", "portocala", "kiwi", "pepene", "mango")
print(thistuple[-4:-1])

output:
(portocala, kiwi, pepene)
```

Dar daca nu exista un element in tuple? Sau nu stim daca un anumit element se afla in tuple-ul noastru? Cum putem verifica daca elementul exista sau nu?

### Putem folosi o conditie **if** pentru a verifica prezenta elementului in tuple.

De exemplu:

```python
thistuple = ("mar", "banana", "cirese")

if "mar" in thistuple:
  print("Da, mar se afla in tuple")

output:
Da, mar se afla in tuple
```

