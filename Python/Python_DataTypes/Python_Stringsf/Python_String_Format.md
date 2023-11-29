# Formatarea string-urilor

Cum am mentionat si pana acum nu putem combina string cu int asa:

```python
number = 24
sentance = "Am varsta de " + number

print(sentance)


output:
Traceback (most recent call last):
  File "Numele fisierului", line 2, in <module>
    txt = "Am varsta de " + number
TypeError: must be str, not int
```

Primim o eroare deoarece nu putem combina o valoare textuala cu una numerica in acest fel. Pentru ca acest lucru sa fie posibil putem folosii functia .fromat():

**Functia .format() preia argumentele transmise, le formateaza si le pune in locul locurilor marcate cu "{}" intr-un array.**

```python
number = 24
sentance = "Am varsta de {} de ani"

print(sentance.format(number))

output:
Am varsta de 24 de ani
```

Cu functia .format() putem adauga un numar nelimitat de argumente atata timp cat acestea sunt egale cu numarul acoladelor din text.

Exemplu:

```python
cantitate = 3
numele_produsului = "mere"
pret = 22.33

comanda_mea = "Am cumparat {} {} la un pret de {}."

print(comanda_mea.format(cantitate, numele_produsului, pret))

output:
Am cumparat 3 mere la un pret de 22.33
```

Dar daca am fi gresit ordinea argumentelor? Cum ar fi aratat acest text?

```python
cantitate = 3
numele_produsului = "mere"
pret = 22.33

comanda_mea = "Am cumparat {} {} la un pret de {}."

print(comanda_mea.format(numele_produsului, cantitate, pret))

output:
Am cumparat mere 3 la un pret de 22.33
```

Pentru a evita aceaste problema putem mentiona intre acolade indexul variabilelor. Adica prima variabila initializata reprezinta indexul 0 , urmatoare indexul 1 si tot asa.

```python
cantitate = 3
numele_produsului = "mere"
pret = 22.33

comanda_mea = "Am cumparat {0} {1} la un pret de {2}."

print(comanda_mea.format(numele_produsului, cantitate, pret))

output:
Am cumparat 3 mere la un pret de 22.33
```

Ca un shortcut putem pune "f"(de la format) in fata unui string direct:

```python
cantitate = 3
numele_produsului = "mere"
pret = 22.33

print(f"Am cumparat {cantitate} {numele_produsului} la un pret de {pret}")

output:
Am cumparat 3 mere la un pret de 22.33
```