# Matematica

Python are un set de funcții matematice încorporate, inclusiv un modul extins de matematică, care vă permite să efectuați sarcini matematice pe numere.

## Functii build-in matematice

Funcțiile **min()** și **max()** pot fi utilizate pentru a găsi cea mai mică sau cea mai mare valoare într-un iterabil:
```python
x = min(5, 10, 25)
y = max(5, 10, 25)

print(x)
print(y)

output:
5
25
```

Funcția abs() returnează valoarea absolută (pozitivă) a numărului specificat:

```python
x = abs(-7.25)

print(x)

output:
7.25
```

Funcția pow(x, y) returnează valoarea lui x la puterea lui y (x^y).

```python
x = pow(4, 3)

print(x)

output:
64
```

## Modulul math

Python are, de asemenea, un modul încorporat numit math, care extinde lista de funcții matematice.

Pentru a-l folosi, trebuie să importați modulul de matematică:

```python
import math
```

După ce ați importat modulul de matematică, puteți începe să utilizați metode și constante ale modulului.

Metoda **math.sqrt()** de exemplu, returnează rădăcina pătrată a unui număr:

```python
import math

x = math.sqrt(64)

print(x)

output:
8.0
```

Metoda** math.ceil()** rotunjește un număr în sus la cel mai apropiat număr întreg, iar metoda **math.floor()** rotunjește un număr în jos la cel mai apropiat număr întreg și returnează rezultatul:

```python
import math

x = math.ceil(1.4)
y = math.floor(1.4)

print(x) 
print(y) 

output:
2
1
```

The math.pi constant, returns the value of PI (3.14...):

```python
import math

x = math.pi

print(x)

output:
3.14
```

