# Set

### Set-urile reprezinta o structura de date care este folosita pentru a stoca mai multe elemente intr-o singura variabila.

### Un set este o colecție neordonată, neschimbată* și neindexată.

### Set-ul se declara intre acolade.

De exemplu:

```python
my_set = {1,2,3,4}

print(my_set)

output:
{1,2,3,4}
```

### Elementele setate pot apărea într-o ordine diferită de fiecare dată când le utilizați și nu pot fi menționate prin index sau cheie.

### Set-ul nu permite exitenta elementelor dublicate!

De exemplu:

```python
thisset = {"mar", "banana", "cirese", "mar"}

print(thisset)

output:
{"mar", "banana", "cirese"}
```

Pentru un set valoarea _True_ si 1 sunt egale, la fel si _False_ cu 0.

De exemplu:

```python
set1 = {"mar", "banana", "cirese", True, 1, 2}
set2 = {"mar", "banana", "cirese", False, True, 0}

print(set1)
print(set2)

output:
{"mar", "banana", "cirese", True, 2}
{"mar", "banana", "cirese", False, True}
```

### Aflarea lungimii unui set folosind functia len()

```python
my_set = {"mar", "banana", "cirese"}

print(len(my_set))

output:
3
```

### Set-urile pot tine toate tipurile de date la fel ca si listele.

```python
set1 = {"mar", "banana", "cirese"}
set2 = {1, 5, 7, 9, 3}
set3 = {True, False, False}
set4 = {1,2,3, "mar", "banana", "cirese", True, False}
```

### O alta metoda de a construii un set este prin folosirea constructorului set()

```python
my_set = set(("mar", "banana", "cirese"))

print(my_set)

output:
{"mar", "banana", "cirese"}
```