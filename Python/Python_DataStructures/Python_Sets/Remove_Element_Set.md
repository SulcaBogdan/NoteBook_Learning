# Stergerea elementelor din set

### Pentru a sterge elementele din set putem folosii metodele .remove() sau .discard()

Exemplu remove():

```python
my_set = {1,2,3,4,5}

my_set.remove(3)

print(my_set)

output:
{1,4,2,5}
```

Exemplu discard():

```python
my_set = {1,2,3,4,5}

my_set.remove(3)

print(my_set)

output:
{1,5,2,4}
```

**Singura diferenta dintre cele doua metode este ca atunci cand un element-ul nu exista in set atunci metoda .remove() va arunca o eroare iar .discard() pur si simplu va ignora si nu va afisa nimic.**

### Putem folosii si metoda .pop() pentru a elimina un element random (deoarece set-ul este o colectie de elemente neordonate care isi schimba pozitia.)

```python
my_set = {"mar", "banana", "cirese"}

x = my_set.pop()

print(x)

print(my_set)

output:
cirese
{"banana", "mar"}
```

### Daca dorim sa golim set-ul complet folosim metoda .clear()

```python 
my_set = {"mar", "banana", "cirese"}
my_set.clear()

print(my_set)

output:
set()
```

### Pentru a sterge definitiv set ul folosim cuvantul cheie 'del'

```python
my_set = {"mar", "banana", "cirese"}
del my_set

print(my_set)

output:
Traceback (most recent call last):
  File "[Your file]", line 5, in <module>
    print(my_set) #this will raise an error because the set no longer exists
NameError: name 'my_set' is not defined
```