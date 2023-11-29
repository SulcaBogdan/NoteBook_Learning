# Concatenarea Stringurilor

Pentru inceput ce inseamna a concatena?

**Concatenarea se refera la operatia de a combina doua sau mai multe siruri sau secvente intr-unul singur.**

### Cum se executa concatenarea?

In acest exemplu am concatenat doua string-uri folosind operatorul '+', dar rezultatul este un singur cuvant, deoarece nu exista un spatiu intre cele doua cuvinte.

```python
a = "Vreau"
b = "mancare"
c = a + b
print(c)

output:
Vreaumancare
```

### Pentru a concatena si cu un spatiu intre cele doua cuvinte folosim **""** 

```python
a = "Vreau"
b = "mancare"
c = a + " " + b
print(c)

output:
Vreau mancare
```

### O alta metoda de a concatena se poate realiza prin folosirea functiei .join():

```python
#Folosirea lui .join() pentru a concatena elementele unei liste
lista = ["Vreau", "sa", "fiu", "programator"]

separator = " "
noul_string = separator.join(lista)

print(noul_string)

output:
Vreau sa fiu programator
```

sau

```python
a = "Vreau"
b = "mancare"

separator = " "

noul_sir = separator.join([a,b])

print(noul_sir)

output:
Vreau mancare
```

### Separatorul 

```python
# Exemplu de utilizare a metodei join() cu diferite separatoare

variabila1 = "Hello"
variabila2 = "World"

# Virgulă
separator_coma = ","
output_coma = separator_coma.join([variabila1, variabila2])

# Linie nouă
separator_newline = "\n"
output_newline = separator_newline.join([variabila1, variabila2])

# Linie goală
separator_empty = ""
output_empty = separator_empty.join([variabila1, variabila2])

# Simbol de plus
separator_plus = "+"
output_plus = separator_plus.join([variabila1, variabila2])

# Underscore
separator_underscore = "_"
output_underscore = separator_underscore.join([variabila1, variabila2])

# Afișare rezultate
print("Virgulă:", output_coma)
output: Hello,World

print("Linie nouă:", output_newline)
output: 
Hello
World

print("Linie goală:", output_empty)
output: HelloWorld

print("Simbol de plus:", output_plus)
output: Hello+World

print("Underscore:", output_underscore)
output: Hello_World
```
How string uses separators with .join() function. 

<div style="text-align:center;">
  <img src="https://i.postimg.cc/TwZfX4hj/push-it-mr-bean.gif" alt="Procedural Programming" >
</div>