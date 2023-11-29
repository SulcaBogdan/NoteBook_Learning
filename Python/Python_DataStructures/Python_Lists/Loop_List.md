# Modalitati de a trece printr-o lista

### for loop

```python
lista = [1,2,3,4]

for x in lista:
    print(x)

output:
1
2
3
4   
```

### for loop index

Prin len(lista) aflam lungimea listei adica 5 si for loop-ul se va repeta de 5 ori incepand de la 0

```python
lista = [1,2,3,4,5]

for x in len(lista):
    print(lista[x])
    
output:
1
2
3
4
5
```

### while loop

Pentru a folosii un while loop trebuie sa creeam o conditie care la un moment dat trebuie sa fie implinita pentru a oprii loop-ul. Daca nu se implineste vom ramane cum un loop infinit si asta poate creea probleme.

Asadar declaram variabila i si o initializam cu val 0. Apoi spunem ca in timp ce i < 4(lungimea listei) executa blocul de cod. In interiorul blocului de cod am incrementat pe i cu 1 dupa fiecare loop. Intr-un final ajungem la 4 < 4 care este False si loop ul se opreste.

```python
lista = [1,2,3,4]
i = 0
while i < len(lista):
    print(lista[i])
    i += 1

output:
1
2
3
4
```

### List Comprehension loop
```python
lista = [1,2,3,4,5]

#Sintaxa [nou_element for element in iterable if conditie]
#Aici spunem ca sa printam x pentru x in lista . Adica sa printam fiecare element din lista.
[print(x) for x in lista]

output:
1
2
3
4
5
```

