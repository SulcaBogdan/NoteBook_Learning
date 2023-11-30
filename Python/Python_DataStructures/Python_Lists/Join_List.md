# Unirea listelor

### Sunt mai multe feluri de a unii doua liste in Python.
Una din cele mai usoare metode este prin folosirea operatorului "+"

Exemplu

```python
list1 = [1,2,3]
list2 = [4,5,6]

new_list = list1 + list2

print(new_list)

output:
[1,2,3,4,5,6]
```

### Prin for loop

Exemplu:
```python
list1 = [1,2,3]
list2 = [4,5,6]

for x in lista2:
    lista1.append(x)

print(list1)

output:
[1,2,3,4,5,6]
```

### Putem folosii si metoda extend() pentru a unii doua liste

Exemplu:
```python
list1 = [1,2,3]
list2 = [4,5,6]

list1.extend(list2)

print(list1)

output:
[1,2,3,4,5,6]
```