# Unirea set-urilor

Sunt cateva metode de a unii doua sau mai multe set-uri in Python.

Putem folosii metoda union() care returneaza un nou set care contine toate elementele set-urilor combinate sau metoda update() pentru a insera elementele unui set in celalalt.

Exemplu union():

```python
set1 = {"a", "b" , "c"}
set2 = {1, 2, 3}

set3 = set1.union(set2)
print(set3)

output:
{"a", 2, "c", "b", 1, 3}
```

Exemplu update():
```python
set1 = {"a", "b" , "c"}
set2 = {1, 2, 3}

set3 = set1.union(set2)
print(set3)

output:
{"c", 3, "a", "b", 1, 2}
```


### Daca dorim sa unim doua set-uri pe un element comun putem folosii metoda 'intersection_update()'

Exemplu:

```python
x = {"mar", "banana", "cirese"}
y = {"google", "microsoft", "mar"}

x.intersection_update(y)

print(x)

output:
{'mar'}
```

Metoda intersection() va returna un nou set, care conține doar elementele care sunt prezente în ambele seturi.

```python
x = {"mar", "banana", "cirese"}
y = {"google", "microsoft", "mar"}

z = x.intersection(y)

print(z)

output:
{'mar'}
```

### Daca dorim sa tinem toate elementele dar fara cele comune atunci folosim metoda symmetric_difference_update()

```python
x = {"mar", "banana", "cirese"}
y = {"google", "microsoft", "mar"}

x.symmetric_difference_update(y)

print(x)

output:
{'google', 'banana', 'microsoft', 'cirese'}
```


The symmetric_difference() method will return a new set, that contains only the elements that are NOT present in both sets.

```python
x = {"mar", "banana", "cirese"}
y = {"google", "microsoft", "mar"}

z = x.symmetric_difference(y)

print(z)

output:
{'google', 'banana', 'microsoft', 'cirese'}
```