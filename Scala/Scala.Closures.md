# Closures in Scala

Un `closure` este o funcție, a cărei valoare returnată depinde de valoarea uneia sau mai multor variabile declarate în afara acestei funcție.

Următoarea bucată de cod cu funcție anonimă.

```scala
val multiplier = (i:Int) => i * 10
```
Aici singura variabilă utilizată în corpul funcției, `i * 10` , este `i`, care este definită ca un parametru al funcției. Încercați următorul cod −

```scala
val multiplier = (i:Int) => i * factor
```

Există două variabile libere în multiplicator: `i` și `factor`. Unul dintre ele, `i`, este un parametru formal al funcției. Prin urmare, este legat la o nouă valoare de fiecare dată când este apelat multiplicatorul. Cu toate acestea, factorul nu este un parametru formal, atunci ce este acesta? Să mai adăugăm o linie de cod.

```scala
var factor = 3
val multiplier = (i:Int) => i * factor
```

Acum factorul are o referință la o variabilă din afara funcției, dar în domeniul de aplicare. Funcția face referire la factor și își citește valoarea curentă de fiecare dată. Dacă o funcție nu are referințe externe, atunci este trivial închisă asupra ei însăși. Nu este necesar un context extern.

```scala
object Demo {
   def main(args: Array[String]) {
      println( "multiplier(1) value = " +  multiplier(1) )
      println( "multiplier(2) value = " +  multiplier(2) )
   }
   var factor = 3
   val multiplier = (i:Int) => i * factor
}

output:
multiplier(1) value = 3
multiplier(2) value = 6
```