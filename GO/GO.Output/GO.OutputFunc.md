# Funcții de ieșire în Go

Go are trei funcții pentru a afișa text:

- `Print()`
- `Println()`
- `Printf()`

## Funcția `Print()`

Funcția `Print()` afișează argumentele sale cu formatul lor implicit.

### Exemplu

Imprimarea valorilor variabilelor `i` și `j`:

```go
package main

import ("fmt")

func main() {
    var i, j string = "Hello", "World"

    fmt.Print(i)
    fmt.Print(j)
}
```

**Rezultat**:
```
HelloWorld
```

---

Dacă dorim să afișăm argumentele pe linii noi, trebuie să folosim `\n`.

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i, j string = "Hello", "World"

    fmt.Print(i, "\n")
    fmt.Print(j, "\n")
}
```

**Rezultat**:
```
Hello
World
```

> **Sfat**: `\n` creează linii noi.

---

Este posibil să folosim o singură funcție `Print()` pentru a afișa mai multe variabile.

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i, j string = "Hello", "World"

    fmt.Print(i, "\n", j, "\n")
}
```

**Rezultat**:
```
Hello
World
```

---

Dacă dorim să adăugăm un spațiu între argumentele de tip string, trebuie să folosim `" "`.

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i, j string = "Hello", "World"

    fmt.Print(i, " ", j)
}
```

**Rezultat**:
```
Hello World
```

---

Funcția `Print()` inserează un spațiu între argumente dacă niciunul dintre ele nu este un șir de caractere.

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i, j = 10, 20

    fmt.Print(i, j)
}
```

**Rezultat**:
```
10 20
```

---

## Funcția `Println()`

Funcția `Println()` este similară cu `Print()`, cu diferența că un spațiu este adăugat între argumente, iar o linie nouă este adăugată la final.

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i, j string = "Hello", "World"

    fmt.Println(i, j)
}
```

**Rezultat**:
```
Hello World
```

---

## Funcția `Printf()`

Funcția `Printf()` formatează mai întâi argumentul său pe baza verbului de formatare dat și apoi îl afișează.

Vom folosi doi verburi de formatare:

- `%v` este folosit pentru a afișa valoarea argumentelor
- `%T` este folosit pentru a afișa tipul argumentelor

### Exemplu

```go
package main

import ("fmt")

func main() {
    var i string = "Hello"
    var j int = 15

    fmt.Printf("i has value: %v and type: %T\n", i, i)
    fmt.Printf("j has value: %v and type: %T\n", j, j)
}
```

**Rezultat**:
```
i has value: Hello and type: string
j has value: 15 and type: int
```



