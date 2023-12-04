# Adaugarea elementelor in dictionar

Pentru a adauga elemente noi in dictionar pur si simplu declaram o cheie noua si valoare ei prin apelarea dictionarului.

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

dictionar["color"] = "red"

print(dictionar)

output:
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
```

## Update

Metoda update() va actualiza dicționarul cu elementele dintr-un argument dat. Dacă articolul nu există, acesta va fi adăugat.

Argumentul trebuie să fie un dicționar sau un obiect iterabil cu perechi cheie:valoare.

```python
dictionar = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
dictionar.update({"color": "red"})

print(dictionar)

output:
{'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
```

