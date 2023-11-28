# Strings sunt arrays. Ce inseamna asta?

Un array este o coletie de elemente, care sunt stocate intr-o secventa ordonata si pot fi accesate prin intermediul unor indici(index) numerici sau chei.

Si cum o valoare textuala poate fi un array? De exemplu cuvantul "Masina"?

Exemplu cod:

```python
#Initializam variabila cu o valoare textuala si o printam
cuvant = "Masina"
print(cuvant)

output:
Masina
---------------------------------------------------------
#Printam doar prima litera din cuvant
print(cuvant[0])

output:
M
```
Deci cand spunem ca un String este un array defapt ne referim la :

Masina = ["M", "a", "s", "i", "n", "a"] 
|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
| M | a | s | i | n | a |
| 0 | 1 | 2 | 3 | 4 | 5 |

Numaratoare la arrays in programare incepe de la indexul 0. Deci lungimea unui array != cu numarul indexurilor.

## String slicing

Putem returna un interval de caractere utilizind sintaxa slice:

[start:end]    

Parantezele patrate pot fi folosite pentru a accesa elementele array ului. 

Exemplu de cod:

```python
#Initializam doua variabile un cu o propozitie si a doua cu primul text sliced incepand de la indexul 4 si oprindu se la indexul 12
cuvant = "Masina este smechera"
cuvant_sliced = cuvant[4:12]

print(cuvant_sliced)

output:
na este
```

### Putem da slice de la inceput:

Exemplu de cod:
```python
cuvant = "Sunt programator"
print(cuvant[:4])

output:
Sunt
```



### Putem da slice pana la final:

Exemplu de cod:
```python
cuvant = "Sunt programator"
print(cuvant[4:])

output:
programator
```

### Putem folosi si negative indexing

Ultimul element dintr-un array poate fi notat si cu -1 iar de acolo sa se inceapa numaratoarea inversa, adica -2, -3 pana la sfarsit(inceput).

|    |    |    |    |    |    |
|----|----|----|----|----|----|
| M  | a  | s  | i  | n  | a  |
| -6 | -5 | -4 | -3 | -2 | -1 |


Exemplu de cod:

```python
cuvant = "Animal"
print(cuvant[-3:-1])

output:
ma
```