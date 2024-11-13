

# Reguli de denumire a variabilelor în Go

O variabilă poate avea un nume scurt (cum ar fi `x` și `y`) sau un nume mai descriptiv (de exemplu: `age`, `price`, `carName`, etc.).

Reguli de denumire a variabilelor în Go:

- Un nume de variabilă trebuie să înceapă cu o literă sau cu caracterul underscore (`_`).
- Un nume de variabilă nu poate începe cu o cifră.
- Un nume de variabilă poate conține doar caractere alfanumerice și underscore-uri (`a-z`, `A-Z`, `0-9`, și `_`).
- Numele variabilelor sunt case-sensitive (de exemplu, `age`, `Age` și `AGE` sunt variabile diferite).
- Nu există o limită de lungime pentru numele variabilei.
- Numele variabilei nu poate conține spații.
- Numele variabilei nu poate fi un cuvânt rezervat în Go.

---

## Nume de variabile compuse din mai multe cuvinte

Numele de variabile formate din mai multe cuvinte pot fi dificil de citit.

Există mai multe tehnici pe care le puteți utiliza pentru a le face mai lizibile:

### Camel Case

Fiecare cuvânt, cu excepția primului, începe cu literă mare:

```go
myVariableName := "John"
```

### Pascal Case

Fiecare cuvânt începe cu literă mare:

```go
MyVariableName := "John"
```

### Snake Case

Fiecare cuvânt este separat de un underscore (`_`):

```go
my_variable_name := "John"
```

