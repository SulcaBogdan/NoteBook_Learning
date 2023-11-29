# Stergerea unui element din lista

### Pentru a sterge un elemente dintr-o lista folosim functia .remove()

```python
lista = ["Dodan", "Bogdan", "Masina"]
lista.remove("Dodan")

print(lista)

output:
["Bogdan", "Masina"]
```
Daca elementul specificat ca parametru in functia .remove() se regaseste de mai multe ori in lista, atunci doar primul element intalnit va fi sters.

```python
lista = ["Dodan", "Dodan", "Bogdan", "Masina"]
lista.remove("Dodan")

print(lista)

output:
["Dodan", "Bogdan", "Masina"]
```

### Stergerea unui element dupa index

```python
lista = ["Dodan", "Bogdan", "Masina"]
lista.pop(1)

print(lista)

output:
["Dodan", "Masina"]
```

**Daca nu specificam un index ca argument pentru functia pop() atunci se va sterge ultimul element din lista**

```python
lista = ["Dodan", "Bogdan", "Masina"]
lista.pop()

print(lista)

output:
["Dodan", "Bogdan"]
```

### Putem folosii si cuvantul-cheie **del** pentru a sterge un element dupa index

```python
lista = ["Dodan", "Bogdan", "Masina"]
del lista[0]

print(lista)

output:
["Bogdan", "Masina"]
```

Cuvantul cheie del poate sterge intreaga lista astfel:

```python
lista = ["Dodan", "Bogdan", "Masina"]
del lista
```