# if ... else conditii si statements

### Python acceptă condițiile logice obișnuite din matematică:

| Operație                    | Descriere                                  | Exemplu              |
|-----------------------------|--------------------------------------------|----------------------|
| Equals: `a == b`            | Verifică dacă a este egal cu b             | `1 == 1` va fi `True` |
| Not Equals: `a != b`        | Verifică dacă a nu este egal cu b          | `1 != 2` va fi `True` |
| Less than: `a < b`          | Verifică dacă a este mai mic decât b       | `1 < 2` va fi `True`  |
| Less than or equal to: `a <= b` | Verifică dacă a este mai mic sau egal cu b | `1 <= 2` va fi `True` |
| Greater than: `a > b`       | Verifică dacă a este mai mare decât b      | `2 > 1` va fi `True`  |
| Greater than or equal to: `a >= b` | Verifică dacă a este mai mare sau egal cu b | `2 >= 1` va fi `True` |


Aceste condiții pot fi utilizate în mai multe moduri, cel mai frecvent în if statement  și loop-uri.

Un if statement este scris folosind cuvântul cheie **'if'**.

De exemplu:

```python
a = 33
b = 200

if b > a:
  print("b este mai mare ca a")

output:
b este mai mare ca a
```
In acest exemplu am initializat doua variabile a si b cu valorile 33 si 200, apoi am scris un if statement cu conditia ca b sa fie mai mare ca a. Daca aceasta conditie este indeplinita(True) atunci se va printa textul din blocul if. Daca nu se va indeplini aceasta conditie atunci nu se va printa nimic.

## Indentare

Python se bazează pe indentare (spații albe la începutul unei linii) pentru a defini domeniul de aplicare în cod. Alte limbaje de programare folosesc adesea paranteze în acest scop.

Exemplu if statement fara identare:

```python
a = 33
b = 200
if b > a:
print("b is greater than a") # o sa primim o eroare

output:
File "[your file]", line 4
    print("b is greater than a")
        ^
IndentationError: expected an indented block
```

## Elif

Cuvântul cheie elif este modul Python de a spune „dacă condițiile anterioare nu erau adevărate, atunci încercați această condiție”.

Exemplu:

```python
a = 33
b = 33
if b > a:
  print("b este mai mare ca a")
elif a == b:
  print("a si b sunt egale")

output:
a si b sunt egale
```

In acest exemplu am initializat 2 variabile a si b cu valorile 33 si 33, apoi am scris un if statement cu prima conditie ca b sa fie mai mare ca a. Daca este True atunci se printeaza primul print iar daca nu se verifica urmatoare conditie elif sau (else if in alte limbaje). A doua conditie este ca a sa fie egal cu b ceea ce este True si se printeaza textul respectiv.

## Else

Cuvântul cheie else prinde orice nu este prins de condițiile precedente.

```python
a = 200
b = 33
if b > a:
  print("b este mai mare ca a")
elif a == b:
  print("a si b sunt egale")
else:
    print("a este mai mare ca b")

output:
a este mai mare ca b
```

In acest exemplu daca nici o conditie nu este indeplinita atunci 'else' o sa inchida if statement-ul si va returna ceva.

## Short Hand If

Dacă aveți o singură instrucțiune de executat, o puteți pune pe aceeași linie cu if statement.


```python
a = 200
b = 33

if a > b: print("a este mai mare ca b")

output:
a este mai mare ca b
```

## Short Hand If ... Else

Dacă aveți o singură instrucțiune de executat, una pentru if și una pentru else, puteți pune totul pe aceeași linie:

```python
a = 2
b = 330

print("A") if a > b else print("B")

output:
B
```

### You can also have multiple else statements on the same line:

```python
a = 330
b = 330

print("A") if a > b else print("=") if a == b else print("B")

output:
=
```

## And

Cuvântul cheie 'and' este un operator logic și este folosit pentru a combina instrucțiuni condiționale:

```python
a = 200
b = 33
c = 500
if a > b and c > a:
  print("Ambele conditii sunt True")

output:
Ambele conditii sunt True
```

## Or

Cuvântul cheie 'or' este un operator logic și este folosit pentru a combina instrucțiuni condiționale:


```python
a = 200
b = 33
c = 500
if a > b or a > c:
  print("Cel putin o conditie este adevarata")

output:
Cel putin o conditie este adevarata
```

## Not

Cuvântul cheie 'not' este un operator logic și este folosit pentru a inversa rezultatul instrucțiunii condiționate:

```python
a = 33
b = 200
if not a > b:
  print("a nu este mai mare ca b")

output:
a nu este mai mare ca b
```

# Nested If

Puteți avea  if statement în interiorul unui if statement, aceasta se numește  nested if statements.

```python
x = 41

if x > 10:
  print("Peste 10,")
  if x > 20:
    print("si peste 20!")
  else:
    print("dar nu peste 20.")

output:
Peste 10,
si peste 20!
```

## pass statement

if statements nu pot fi goale, dar dacă dintr-un motiv oarecare aveți un if statement fără conținut, introduceți 'pass' pentru a evita o eroare.

```python
a = 33
b = 200

if b > a:
  pass

# având un if statement gol ca aceasta, ar genera o eroare fără instrucțiunea pass
```

