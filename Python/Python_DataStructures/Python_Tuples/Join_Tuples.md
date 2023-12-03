# Legarea tuple-urilor

### Pentru a lega/unii doua tuple putem folosii '+':

```python
tuple1 = ("a", "b" , "c")
tuple2 = (1, 2, 3)

tuple3 = tuple1 + tuple2
print(tuple3)

output:
("a", "b" , "c", 1, 2, 3)
```

### Daca dorim sa multiplicam elementele din tupla noastra putem folosii operatorul '*':

```python
fruits = ("apple", "banana", "cherry")
mytuple = fruits * 2

print(mytuple)
("apple", "banana", "cherry", "apple", "banana", "cherry")
```