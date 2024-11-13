
# Variabile în Go

Variabilele sunt containere pentru stocarea valorilor de date.

## Tipuri de variabile în Go

În Go, există diferite tipuri de variabile, de exemplu:

- `int` - stochează întregi (numere întregi), precum 123 sau -123.
- `float32` - stochează numere cu virgulă mobilă, cu zecimale, precum 19.99 sau -19.99.
- `string` - stochează text, precum "Hello World". Valorile de tip string sunt înconjurate de ghilimele.
- `bool` - stochează valori cu două stări: adevărat sau fals.

Mai multe detalii despre tipurile de variabile vor fi explicate în capitolul **Go Data Types**.

## Declararea (Crearea) Variabilelor

În Go, există două moduri de a declara o variabilă:

1. Cu cuvântul cheie `var`:

   Folosiți cuvântul cheie `var`, urmat de numele variabilei și tipul acesteia.

   ### Sintaxă

   ```go
   var numeVariabila tip = valoare
   ```

   > **Notă**: Trebuie să specificați întotdeauna fie `tip`, fie `valoare` (sau pe ambele).

2. Cu semnul `:=`:

   Folosiți semnul `:=`, urmat de numele variabilei și valoare.

   ### Sintaxă

   ```go
   numeVariabila := valoare
   ```

   > **Notă**: În acest caz, tipul variabilei este dedus din valoare (asta înseamnă că compilatorul decide tipul variabilei pe baza valorii).

> **Observație**: Nu este posibil să declarați o variabilă folosind `:=` fără a-i atribui o valoare.

---

## Declararea variabilelor cu valoare inițială

Dacă valoarea unei variabile este cunoscută de la început, puteți declara variabila și să-i atribuiți o valoare într-o singură linie:

### Exemplu

```go
package main

import ("fmt")

func main() {
    var student1 string = "John" //tipul este string
    var student2 = "Jane"        //tipul este dedus
    x := 2                        //tipul este dedus

    fmt.Println(student1)
    fmt.Println(student2)
    fmt.Println(x)
}
```

> **Notă**: Tipurile variabilelor `student2` și `x` sunt deduse din valorile lor.

---

## Declararea variabilelor fără valoare inițială

În Go, toate variabilele sunt inițializate. Deci, dacă declarați o variabilă fără valoare inițială, valoarea acesteia va fi setată la valoarea implicită a tipului său:

### Exemplu

```go
package main

import ("fmt")

func main() {
    var a string
    var b int
    var c bool

    fmt.Println(a)
    fmt.Println(b)
    fmt.Println(c)
}
```

### Explicația exemplului

În acest exemplu, există 3 variabile:

- `a`
- `b`
- `c`

Aceste variabile sunt declarate, dar nu li s-au atribuit valori inițiale.

Prin rularea codului, putem observa că ele au deja valorile implicite ale tipurilor lor respective:

- `a` este `""` (șir gol)
- `b` este `0`
- `c` este `false`

---

## Atribuirea valorii după declarare

Este posibil să atribuiți o valoare unei variabile după ce a fost declarată. Acest lucru este util pentru cazurile în care valoarea nu este cunoscută inițial.

### Exemplu

```go
package main

import ("fmt")

func main() {
    var student1 string
    student1 = "John"
    fmt.Println(student1)
}
```

> **Notă**: Nu este posibil să declarați o variabilă folosind `:=` fără a-i atribui o valoare.

---

## Diferența între `var` și `:=`

Există câteva diferențe între utilizarea `var` și `:=`:

|                        | `var`                                             | `:=`                                                |
|------------------------|---------------------------------------------------|-----------------------------------------------------|
| Poate fi folosit în interiorul și în afara funcțiilor | Da                                                | Nu                                                  |
| Declarația și atribuirea valorii pot fi făcute separat | Da                                                | Nu (trebuie făcut în aceeași linie)                 |

### Exemplu

Acest exemplu arată declararea variabilelor în afara unei funcții, utilizând cuvântul cheie `var`:

```go
package main

import ("fmt")

var a int
var b int = 2
var c = 3

func main() {
    a = 1
    fmt.Println(a)
    fmt.Println(b)
    fmt.Println(c)
}
```

### Exemplu

Deoarece `:=` este folosit în afara unei funcții, rularea programului va produce o eroare.

```go
package main

import ("fmt")

a := 1

func main() {
    fmt.Println(a)
}
```

**Rezultat**:

```
./prog.go:5:1: syntax error: non-declaration statement outside function body
```

Am analizat imaginile și voi furniza traducerea completă a conținutului despre declarația multiplă de variabile în Go.

---

# Declarația multiplă de variabile în Go

În Go, este posibil să declarați mai multe variabile pe aceeași linie.

### Exemplu

Acest exemplu arată cum să declarați mai multe variabile pe aceeași linie:

```go
package main

import ("fmt")

func main() {
    var a, b, c, d int = 1, 3, 5, 7

    fmt.Println(a)
    fmt.Println(b)
    fmt.Println(c)
    fmt.Println(d)
}
```

> **Notă**: Dacă folosiți cuvântul cheie `type`, este posibil să declarați doar un singur tip de variabilă pe linie.

Dacă cuvântul cheie `type` nu este specificat, puteți declara variabile de tipuri diferite pe aceeași linie:

### Exemplu

```go
package main

import ("fmt")

func main() {
    var a, b, c = 6, "Hello"
    d := 7
    e := "World!"

    fmt.Println(a)
    fmt.Println(b)
    fmt.Println(c)
    fmt.Println(d)
    fmt.Println(e)
}
```

---

# Declarația variabilelor într-un bloc în Go

Declarațiile multiple de variabile pot fi, de asemenea, grupate într-un bloc pentru o lizibilitate mai bună:

### Exemplu

```go
package main

import ("fmt")

func main() {
    var (
        a int
        b int = 1
        c string = "hello"
    )

    fmt.Println(a)
    fmt.Println(b)
    fmt.Println(c)
}
```

