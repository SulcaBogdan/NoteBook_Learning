# Cum se poate trece printr-un Tuple. Folosind loops!!

Vom folosii for loop si while loop pentru exemplele noastre:

**for loop exemplu:**

```python
my_tuple = ("banana", "cirese", "capsuna")
for x in my_tuple:
    print(x)

output:
banana
cirese
capsuna
```

Am folosit for loop direct pe elementele tuplei dar putem face acelasi lucru si dupa index:

Exemplu:

```python
my_tuple = ("banana", "cirese", "capsuna")

for x in range(len(my_tuple)):
    print(my_tuple[x])

output:
banana
cirese
capsuna
```

Puteți parcurge elementele tuple folosind o buclă while.

Utilizați funcția **len()** pentru a determina lungimea tuplului, apoi începeți de la 0 și treceți-vă în buclă prin elementele tuplu, dupa index-ul acestora.

Nu uitați să creșteți indicele cu 1 după fiecare iterație.

**while loop exemplu:**


```python
my_tuple = ("banana", "cirese", "capsuna")
i = 0

while i < len(my_tuple):
    print(my_tuple[i])
    i += 1

output:
banana
cirese
capsuna
```
