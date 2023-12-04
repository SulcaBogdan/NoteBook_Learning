# Copierea dictionarelor

Nu puteți copia un dicționar pur și simplu tastând dict2 = dict1, deoarece: dict2 va fi doar o referință la dict1, iar modificările făcute în dict1 vor fi făcute automat și în dict2.

Există modalități de a face o copie, o modalitate este de a folosi metoda încorporată de Dicționar copy().

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
dictionar_copy = dictionar.copy()
print(dictionar_copy)

output:
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```

### O altă modalitate de a face o copie este să utilizați funcția încorporată dict().

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
dictionar_copy = dict(dictionar)
print(dictionar_copy)

output:
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```

