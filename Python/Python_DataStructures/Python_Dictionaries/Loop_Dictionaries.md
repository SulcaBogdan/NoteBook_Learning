# Trecerea prin dictionar

Puteți parcurge un dicționar folosind o buclă for.

Când treceți în buclă printr-un dicționar, valoarea returnată sunt cheile dicționarului, dar există și metode pentru a returna valorile.


### Tipăriți toate numele cheilor în dicționar, unul câte unul:

```python
dictionar =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
for x in dictionar:
  print(x)

output:
brand
model
year
```

### Tipăriți toate valorile din dicționar, una câte una:

```python
dictionar =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
for x in dictionar:
  print(dictionar[x])

output:
Ford
Mustang
1964
```

### De asemenea, puteți utiliza metoda values() pentru a returna valorile unui dicționar:

```python
dictionar =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
for x in dictionar.values():
  print(x)

output:
Ford
Mustang
1964
```

### Puteți folosi metoda keys() pentru a returna cheile unui dicționar:

```python
dictionar =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
for x in dictionar.keys():
  print(x)

output:
brand
model
year
```

### Căutați în buclă atât cheile, cât și valorile, utilizând metoda items():

```python
dictionar =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
for x, y in dictionar.items():
  print(x,y)

output:
brand Ford
model Mustang
year 1964
```



