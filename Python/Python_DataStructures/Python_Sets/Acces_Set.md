# Accesarea unui element din set sau elemente.

### Nu puteți accesa articole dintr-un set prin referire la un index sau o cheie.

Dar puteți parcurge elementele set folosind o buclă 'for'.

```python
my_set = {"mar", "banana", "cirese"}

for x in my_set:
  print(x)

output:
mar
banana
cirese
```

Sau puteți întreba dacă o valoare specificată este prezentă într-un set, folosind cuvântul cheie 'in'.

```python
my_set = {"mar", "banana", "cirese"}

print("mar" in my_set)

output:
True
```
