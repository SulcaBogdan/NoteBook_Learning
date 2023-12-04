# Stergerea elementelor dintr-un dictionar

Exista mai multe metode de a sterge elemente din dictionar.

### Metoda pop() elimină elementul cu numele cheii specificat:

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

dictionar.pop("model")

print(dictionar)

output:
{'brand': 'Ford', 'year': 1964}
```

### Metoda popitem() elimină ultimul element inserat:

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

dictionar.popitem()

print(dictionar)

output:
{'brand': 'Ford', 'model': 'Mustang'}
```

### Cuvântul cheie 'del' elimină elementul cu numele cheii specificat:

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

del dictionar["model"]

print(dictionar)

output:
{'brand': 'Ford', 'year': 1964}
```

### Cuvântul cheie 'del' poate, de asemenea, șterge complet dicționarul:

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

del dictionar

print(dictionar)

output:
Traceback (most recent call last):
  File "[Your file]", line 7, in <module>
    print(dictionar) #this will cause an error because "dictionar" no longer exists.
NameError: name 'dictionar' is not defined
```

### Metoda clear() golește dicționarul:

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

dictionar.clear()

print(dictionar)

output:
{}
```