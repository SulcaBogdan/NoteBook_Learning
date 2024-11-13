# Tipurile de Date în Go

Tipul de date este un concept important în programare. Tipul de date specifică dimensiunea și tipul valorilor unei variabile.

Go este un limbaj de tip statically typed, ceea ce înseamnă că odată definit un tip de variabilă, aceasta poate stoca doar date de acel tip.

Go are trei tipuri de bază de date:

- `bool`: reprezintă o valoare booleană și poate fi fie `true`, fie `false`
- `Numeric`: reprezintă tipuri întregi, tipuri de numere în virgulă mobilă și tipuri complexe
- `string`: reprezintă o valoare de tip șir de caractere

### Exemplu

Acest exemplu arată câteva dintre diferitele tipuri de date din Go:

```go
package main

import ("fmt")

func main() {
    var a bool = true       // Boolean
    var b int = 5           // Integer
    var c float32 = 3.14    // Floating point number
    var d string = "Hi!"    // String

    fmt.Println("Boolean:", a)
    fmt.Println("Integer:", b)
    fmt.Println("Float:", c)
    fmt.Println("String:", d)
}
```

---
