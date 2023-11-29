# Functiile String

Python dispune de o varietate de functii build-in care pot fi folosite pe string.

De exemplu:

1. upper()

```python
#Initializam variabila cu o valoare textuala string
variabila = "bogdan"

#Printam valoarea textuala cu toate literele mari.
#Functia .upper() face toate literele upper case.
print(variabila.upper())

output:
BOGDAN
```
2. .lower()

```python
variabila = "BOGDAN"

print(variabila.lower())

output:
bogdan
```

3. Stergerea spatiilor goale 

Daca exita spatii goale in text care nu sunt dorite le putem elimina folosind functia .strip():

```python
#Exista un spatiu inaintea primului cuvant
variabila = " Hello, World!"

print(variabila.strip())

output:
Hello, World!
```

4. Inlocuirea unui string

Functia .replace() cauta prin cuvant prima aparitie a lui H ca un loop.

```python
variabila = "Hello World!"

print(variabila.replace("H","J"))

output:
Jello World!
```

5. Despartirea unui string

Functia **.split()** returneaza o lista dupa o conditie/separator(",./!?" etc..).

```python
variabila = "Hello, World!"

#Desparte stringul la fiecare virgula intalnita
print(variabila.split(","))

output:
["Hello", "World!"]
```