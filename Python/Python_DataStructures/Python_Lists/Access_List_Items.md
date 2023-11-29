# Accesarea elementelor din lista

### Elementele unei liste sunt indexate si le putem accesa mentionand indexul acestora din lista.

De exemplu:

```python
#Am initializat lista cu valori numerice
lista = [1,2,3,4]

#Am printat elementul cu indexul 1 din lista
print(lista[1])

output:
2
```

**Numaratoarea incepe mereu de la 0.**

### Putem accesa si dupa indexul negativ.

De exemplu:

```python
lista = [1,2,3,4]
#Am printat elementul cu indexul -1 din lista
print(lista[-1])

output:
4
```

**Numaratoarea inversa a indexilor incepe mereu de la -1.**

### Putem folosi un concept asemanator cu String Slicing ([start:end:pace]) si pentru liste.

De exemplu:

```python
lista = ["Am" , "devenit", "junior", "programator", "!"]

#Incepem printarea de la elementul cu index 2 pana la sfarsit.
print(lista[2:]

output:
["junior", "programator", "!"]
```

### Putem selecta si un interval sau sa inversam la fel prin accesarea indexului negativ.

De exemplu

```python
lista = [1,2,3,4,5]

print(lista[-1:-3])
print(lista[1:4])

output:
[5,4]
[2,3,4]
```

Dar daca nu exista un element in lista? Sau nu stim daca un anumit element se afla in lista noastra? Cum putem verifica daca elementul exista sau nu?

### Putem folosi o conditie **if** pentru a verifica prezenta elementului in lista.

De exemplu:

```python
lista = ["Am" , "devenit", "junior", "programator", "!"]

#Se verifica daca junior este in lista noastra ceea ce este True
if "junior" in lista:
    #Se executa acest bloc de cod deoarece conditia a fost indeplinita!
    print("Da chiar am devenit junior programator") 

output:
Da chiar am devenit junior programator
```

Daca conditia nu ar fi fost indeplinita atunci la output ar fi fost gol. In acel "if statement" se ia conditia pusa de noi respectiv "junior" si o compara cu fiecare element din lista in parte. 

| Expresie           | Rezultat |
|--------------------|----------|
| junior == Am       | False    |
| junior == devenit  | False    |
| junior == junior   | True     |
