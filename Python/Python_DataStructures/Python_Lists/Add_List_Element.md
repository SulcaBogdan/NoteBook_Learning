# Adaugarea unui element in lista

### Pentru a adauga un element la sfarsitul listei folosim functia .append()

```python
lista = [1,2,3,4]

lista.append(5)

print(lista)

output:
[1,2,3,4,5]
```

### Pentru a insera un nou element in lista la un index dorit folosim functia .insert()


```python
lista = [1,3,4,5]

lista.insert(1, 2) # lista.insert(index, element)

print(lista)

output:
[1,2,3,4,5]
```