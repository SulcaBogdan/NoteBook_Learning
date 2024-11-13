# Tipul de Date Boolean în Go

Un tip de date boolean este declarat folosind cuvântul cheie `bool` și poate avea doar valorile `true` sau `false`.

Valoarea implicită pentru un tip de date boolean este `false`.

### Exemplu

Acest exemplu arată câteva modalități diferite de a declara variabile de tip boolean:

```go
package main

import ("fmt")

func main() {
    var b1 bool = true    // declarație cu tip specificat și valoare inițială
    var b2 = true         // declarație fără tip specificat și cu valoare inițială
    var b3 bool           // declarație cu tip specificat fără valoare inițială
    b4 := true            // declarație fără tip specificat și cu valoare inițială

    fmt.Println(b1) // Returnează true
    fmt.Println(b2) // Returnează true
    fmt.Println(b3) // Returnează false (valoare implicită)
    fmt.Println(b4) // Returnează true
}
```

