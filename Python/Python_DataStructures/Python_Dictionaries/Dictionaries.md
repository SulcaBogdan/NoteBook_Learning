# Dictionarele

### Dictionarul este o structura de date ordonata, modificabila si nu permite dublicatele. Acesta este folosit pentru a stoca infomartii sub forma cheie : valoare . 

Dictionarul se initializeaza intre acolade '{ }'

Exemplu:

```python
dictionar = {
    "Dodan":26,
    "Bogdan":25,
    "Andra":30
}

print(dictionar)

output:
{"Dodan":26, "Bogdan":25, "Andra":30}
```

## Elementele Dictionarului

Elementele dictionarului sunt ordonate, cu posibilitatea de a fi schimbate si fara dublicate.

### Pentru a printa un item(value) din dictionar putem scrie numele dictionarului urmat de paranteze patrate si cheia valorii care ne intereseaza

De exemplu:

```python
dictionar = {
    "Dodan":26,
    "Bogdan":25,
    "Andra":30
}

print(dictionar["Dodan"])

output:
26
```

## Ordonat sau neordonat?

Când spunem că dicționarele sunt ordonate, înseamnă că articolele au o ordine definită și această ordine nu se va schimba.

Neordonat înseamnă că articolele nu au o ordine definită, nu vă puteți referi la un articol folosind un index.

## Modificabile

Dicționarele sunt modificabile, ceea ce înseamnă că putem schimba, adăuga sau elimina articole după ce dicționarul a fost creat.

## Fara dublicate

Dicționarele nu pot avea două articole cu aceeași cheie:

```python
dictionar = {
    "Dodan":26,
    "Bogdan":25,
    "Andra":30,
    "Andra":34
}

print(dictionar)

output:
{"Dodan":26, "Bogdan":25, "Andra":34}
```

### Lungimea dictionarului de afla folosind functia len(). Se va returna numarul cheilor din dictionar.


```python
dictionar = {
    "Dodan":26,
    "Bogdan":25,
    "Andra":30
}

print(len(dictionar))

output:
3
```

## Tipurile de date din dictionar

In dictionar putem folosii toate tipurile de date dar si alte structuri de date. 

De exemplu:

```python
dictionar = {
    "Dodan":26,
    "Adevarat?":True,
    "cifre":[1,2,3,4,5]
}
```

### Putem creea un dictionar folosind constructorul acestuia, respectiv dict()


De exemplu:

```python
dictionar = dict(Dodan = 26, Bogdan = 25 , Andra = 30)

print(dictionar)

output:
{"Dodan":26, "Bogdan":25, "Andra":34}
```

Elementele din dictionar vor fi mereu puse sub forma KEY : VALUE


