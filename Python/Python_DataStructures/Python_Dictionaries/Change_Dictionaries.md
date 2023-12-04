# Schimbarea elementelor in dictionare

### Putem schimba o valoare specifica din dictionar folosind cheile

De exemplu:
```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

#Am selectat cheia 'year' din dictionar si i-am modificat valoarea din 1964 in 2018
dictionar["year"] = 2018

print(dictionar)

output:
{'brand': 'Ford', 'model': 'Mustang', 'year': 2018}
```

## Update

Metoda update() va actualiza dicționarul cu elementele din argumentul dat.

Argumentul trebuie să fie un dicționar sau un obiect iterabil cu perechi cheie:valoare.

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
dictionar.update({"year": 2020})

print(dictionar)

output:
{'brand': 'Ford', 'model': 'Mustang', 'year': 2020}
```

