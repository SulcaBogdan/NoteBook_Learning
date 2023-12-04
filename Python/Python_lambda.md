# Python lambda functions

O funcție lambda este o mică funcție anonimă.

O funcție lambda poate lua orice număr de argumente, dar poate avea o singură expresie.

## Syntax
`lambda arguments : expression`

Exemplu:

Adăugați 10 la argumentul a și returnați rezultatul:

```python
x = lambda a : a + 10
print(x(5))

output:
15
```

#### Funcțiile Lambda pot lua orice număr de argumente:

Înmulțiți argumentul a cu argumentul b și returnați rezultatul:

```python
x = lambda a, b : a * b
print(x(5, 6))

output:
30
```

Rezumați argumentele a, b și c și returnați rezultatul:

```python
x = lambda a, b, c : a + b + c
print(x(5, 6, 2))

output:
13
```

## De ce se folosesc functiile lambda?

Puterea lambda este mai bine arătată atunci când le utilizați ca funcție anonimă în interiorul unei alte funcții.

Să presupunem că aveți o definiție a funcției care ia un argument și acel argument va fi înmulțit cu un număr necunoscut:

```python
def functia_mea(n):
  return lambda a : a * n
  ```

Utilizați acea definiție a funcției pentru a crea o funcție care dublează întotdeauna numărul pe care îl trimiteți:

```python
def functia_mea(n):
  return lambda a : a * n

mydoubler = functia_mea(2)

print(mydoubler(11))

output:
22
```

Sau, utilizați aceeași definiție a funcției pentru a crea o funcție care triplează întotdeauna numărul pe care îl trimiteți:

```python
def functia_mea(n):
  return lambda a : a * n

mydoubler = functia_mea(3)

print(mydoubler(11))

output:
33
```



