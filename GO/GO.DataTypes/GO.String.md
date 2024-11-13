# Tipul de Date String în Go

Tipul de date `string` este utilizat pentru a stoca o secvență de caractere (text). Valorile de tip string trebuie să fie înconjurate de ghilimele duble (`"`).

---

### Exemplu

Acest exemplu arată cum să declari și să afișezi variabile de tip `string`:

```go
package main
import ("fmt")

func main() {
    var txt1 string = "Hello!"
    var txt2 string
    txt3 := "World 1"

    fmt.Printf("Tip: %T, valoare: %v\n", txt1, txt1)
    fmt.Printf("Tip: %T, valoare: %v\n", txt2, txt2)
    fmt.Printf("Tip: %T, valoare: %v\n", txt3, txt3)
}
```

**Rezultatul:**
```
Tip: string, valoare: Hello!
Tip: string, valoare:
Tip: string, valoare: World 1
```

---