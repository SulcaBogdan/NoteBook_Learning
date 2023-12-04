# Accesarea elementelor din dictionar

Puteți accesa articolele unui dicționar referindu-vă la numele cheii acestuia, între paranteze drepte:

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
x = thisdict["model"]

print(x)

output:
Mustang
```

### Putem selecta o valoare exact ca exemplul de sus folosind si metoda get()

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
x = thisdict.get("model")

print(x)

output:
Mustang
```

## Afisarea cheilor

Metoda keys() va returna o listă cu toate cheile din dicționar.

Exemplu:

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
x = thisdict.keys()

print(x)

output:
dict_keys(['brand', 'model', 'year'])
```

Lista cheilor este o vizualizare a dicționarului, ceea ce înseamnă că orice modificări aduse dicționarului vor fi reflectate în lista de chei.

Exemplu:

```python
car = {
"brand": "Ford",
"model": "Mustang",
"year": 1964
}

x = car.keys()

print(x) #inainte de schimbare

car["color"] = "white"

print(x) #dupa schimbare

output:
dict_keys(['brand', 'model', 'year'])
dict_keys(['brand', 'model', 'year', 'color'])
```

## Afisarea valorilor

Metoda values() va returna o listă cu toate valorile din dicționar.

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
x = thisdict.values()

print(x)

output:
dict_values(['Ford', 'Mustang', 1964])
```

Lista de valori este o vizualizare a dicționarului, ceea ce înseamnă că orice modificări aduse dicționarului vor fi reflectate în lista de valori.

```python
car = {
"brand": "Ford",
"model": "Mustang",
"year": 1964
}

x = car.values()

print(x) #inainte de schimbare

car["year"] = 2020

print(x) #dupa schimbare

output:
dict_values(['Ford', 'Mustang', 1964])
dict_values(['Ford', 'Mustang', 2020])
```

```python
car = {
"brand": "Ford",
"model": "Mustang",
"year": 1964
}

x = car.values()

print(x) #inainte de schimbare

# Adaugarea unei noua chei cu valoarea "red"
car["color"] = "red"

print(x) #dupa schimbare

output:
dict_values(['Ford', 'Mustang', 1964])
dict_values(['Ford', 'Mustang', 1964, 'red'])
```

## Afisarea perechilor cheie : valoare

Metoda items() va returna fiecare articol dintr-un dicționar, ca tupluri într-o listă.

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

x = thisdict.items()

print(x)

output:
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
```

Lista returnată este o vizualizare a articolelor din dicționar, ceea ce înseamnă că orice modificări aduse dicționarului vor fi reflectate în lista de articole.

```python
car = {
"brand": "Ford",
"model": "Mustang",
"year": 1964
}

x = car.items()

print(x) #inainte de schimbare

car["year"] = 2020

print(x) #dupa schimbare

output:
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 2020)])
```

```python
car = {
"brand": "Ford",
"model": "Mustang",
"year": 1964
}

x = car.items()

print(x) #inainte de schimbare

car["color"] = "red"

print(x) #dupa schimbare

output:
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964), ('color', 'red')])
```

## Verifica daca o cheie exista

Pentru a determina dacă o cheie specificată este prezentă într-un dicționar, utilizați cuvântul cheie in:

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
if "model" in thisdict:
  print("Da cheia model exista in dictionar")

output:
Da cheia model exista in dictionar
```

