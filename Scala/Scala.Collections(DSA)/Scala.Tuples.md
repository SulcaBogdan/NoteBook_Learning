# Tuple in Scala

Scala `tuple` combină un număr fix de elemente împreună, astfel încât acestea să poată fi transmise ca întreg. Spre deosebire de o array sau o listă, un tuplu poate deține obiecte cu diferite tipuri, dar sunt și imuabile.

Următorul este un exemplu de tuplu care conține un număr întreg, un șir și consola.

```scala
val t = (1, "hello", Console)
```

Care este zahăr sintactic (scurtătură) pentru următoarele −

```scala
val t = new Tuple3(1, "hello", Console)
```

Tipul real al unui `tuplu` depinde de numărul și de elementele pe care le conține și de tipurile acelor elemente. Astfel, tipul de `(99, „Luftballons”)` este `Tuple2[Int, String]`. Tipul de `(„u”, „r”, „the”, 1, 4, „eu”)` este` Tuple6[Char, Char, String, Int, Int, String]`

Tuplurile sunt de tip `Tuple1`, `Tuple2`, `Tuple3` și așa mai departe. În prezent, există o limită superioară de 22 în Scala dacă aveți nevoie de mai mult, atunci puteți utiliza o colecție, nu un tuplu. Pentru fiecare tip `TupleN`, unde `1 <= N <= 22`, Scala definește un număr de metode de acces la elemente. Având în vedere următoarea definiție −

```scala
val t = (4,3,2,1)
```

Pentru a accesa elementele unui tuplu `t`, puteți folosi metoda `t._1` pentru a accesa primul element, `t._2` pentru a accesa al doilea și așa mai departe. De exemplu, următoarea expresie calculează suma tuturor elementelor lui `t`.

```scala
val sum = t._1 + t._2 + t._3 + t._4
```

Puteți folosi Tuple pentru a scrie o metodă care ia o `Listă[Double]` și returnează numărul, suma și suma pătratelor returnate într-un tuplu cu trei elemente, un `Tuple3[Int, Double, Double]`. De asemenea, sunt utile pentru a transmite o listă de valori de date ca mesaje între actori în programarea concomitentă.

Încercați următorul exemplu de program. Arată cum să folosești un tuplu.

```scala
object Demo {
   def main(args: Array[String]) {
      val t = (4,3,2,1)
      val sum = t._1 + t._2 + t._3 + t._4

      println( "Sum of elements: "  + sum )
   }
}

output:
Sum of elements: 10
```

## Iterarea prin Tuple

Puteți utiliza metoda `Tuple.productIterator()` pentru a repeta peste toate elementele unui tuplu.

Încercați următorul exemplu de program pentru a repeta peste tupluri.

```scala
object Demo {
   def main(args: Array[String]) {
      val t = (4,3,2,1)
      
      t.productIterator.foreach{ i =>println("Value = " + i )}
   }
}

output:
Value = 4
Value = 3
Value = 2
Value = 1
```

## Convertirea in string

Puteți folosi metoda `Tuple.toString()` pentru a concatena toate elementele tuplului într-un string. Încercați următorul exemplu de program pentru a converti în String.

```scala
object Demo {
   def main(args: Array[String]) {
      val t = new Tuple3(1, "hello", Console)
      
      println("Concatenated String: " + t.toString() )
   }
}

output:
Concatenated String: (1,hello,scala.Console$@281acd47)
```

## Swap elements

Puteți folosi metoda `Tuple.swap` pentru a schimba elementele unui `Tuple2`.

Încercați următorul exemplu de program pentru a schimba elementele.

```scala
object Demo {
   def main(args: Array[String]) {
      val t = new Tuple2("Scala", "hello")
      
      println("Swapped Tuple: " + t.swap )
   }
}

output:
Swapped tuple: (hello,Scala)
```



