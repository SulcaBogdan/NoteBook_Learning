# Adaugarea elementelor in set

### Daca dorim sa adaugam un element nou in set-ul nostru putem folosii metoda .add()

De exemplu:

```python
my_set = {"mar", "banana", "cirese"}

my_set.add("orange")

print(my_set)

output:
{"mar", "banana", "cirese", "orange"}
```

### Pentru a adauga alte elemente dintr-un alt set in set-ul initial putem folosii metoda .update()

De exemplu:

```python
my_set1 = {"mar", "banana", "cirese"}
my_set2 = {"para", "struguri", "fructul pasiunii"}

my_set1.update(my_set2)

print(my_set1)

output:
{"mar", "banana", "cirese", "orange", "para", "struguri", "fructul pasiunii"}
```

**NOTE** Dupa fiecare print elementele din set se amesteca, aceasta fiind o caracteristica a set-urilor.

Folosind metoda .update() putem adauga set-ului nostru orice obiect iterabil -> liste tuple etc..

```python
my_set = {"mar", "banana", "cirese"}
my_list = ["para", "struguri"]

my_set.update(my_list)

print(my_set)

output:
{"mar", "banana", "cirese", "orange", "para", "struguri"}
```