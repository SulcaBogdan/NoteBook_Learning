# Copierea unei liste

Nu puteți copia o listă doar tastând list2 = list1, deoarece: list2 va fi doar o referință la list1, iar modificările făcute în list1 vor fi făcute automat și în list2.

### Una din metodele de a copia o lista este prin folosirea metodei .copy()

Exemplu:

```python
lista = [1,2,3]
lista_noua = lista.copy()

print(lista_noua)

output:
[1,2,3]
```

### Alta metoda ar fi prin utilizarea metodei build-in list()

Exemplu:
```python
lista = [1,2,3]
lista_noua = list(lista)

print(lista_noua)

output:
[1,2,3]
```