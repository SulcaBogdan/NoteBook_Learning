# Map in Scala

 Scala `Map` este o colecție de perechi cheie/valoare. Orice valoare poate fi preluată pe baza cheii sale. Cheile sunt unice în `Map`, dar valorile nu trebuie să fie unice.
 
  Maps sunt numite și tabele `Hash`. Există două tipuri de `maps`, cele **imuabile** și cele **mutabile**. Diferența dintre obiectele mutabile și imuabile este că atunci când un obiect este imuabil, obiectul în sine nu poate fi schimbat.

Implicit, Scala folosește `map imuabilă`. Dacă doriți să utilizați `map mutabilă`, va trebui să importați în mod explicit clasa scala.`collection.mutable.Map`. Dacă doriți să utilizați atât maps mutabile, cât și maps imuabile în același timp, atunci puteți continua să vă referiți la Harta imuabilă ca map, dar vă puteți referi la setul mutabil ca maps mutabile.

Următoarele sunt exemple de declarații pentru a declara Maps imuabile −

```scala
// Empty hash table whose keys are strings and values are integers:
var A:Map[Char,Int] = Map()

// A map with keys and values.
val colors = Map("red" -> "#FF0000", "azure" -> "#F0FFFF")
```
În timpul definirii map goale, adnotarea tipului este necesară deoarece sistemul trebuie să aloce un tip concret variabilei. Dacă vrem să adăugăm o pereche cheie-valoare la un map, putem folosi operatorul `+` după cum urmează.

```scala
A + = ('I' -> 1)
A + = ('J' -> 5)
A + = ('K' -> 10)
A + = ('L' -> 100)
```

## Operatiuni basi pe Map

| Nr.  | Metodă           | Descriere                                                                                   |
|------|------------------|--------------------------------------------------------------------------------------------|
| 1    | `keys`           | Această metodă returnează un obiect iterabil care conține fiecare cheie din harta map.    |
| 2    | `values`         | Această metodă returnează un obiect iterabil care conține fiecare valoare din harta map.  |
| 3    | `isEmpty`        | Această metodă returnează `true` dacă harta map este goală și `false` în caz contrar.    |

```scala
object Demo {
   def main(args: Array[String]) {
      val colors = Map("red" -> "#FF0000", "azure" -> "#F0FFFF", "peru" -> "#CD853F")

      val nums: Map[Int, Int] = Map()

      println( "Keys in colors : " + colors.keys )
      println( "Values in colors : " + colors.values )
      println( "Check if colors is empty : " + colors.isEmpty )
      println( "Check if nums is empty : " + nums.isEmpty )
   }
}

output:
Keys in colors : Set(red, azure, peru)
Values in colors : MapLike(#FF0000, #F0FFFF, #CD853F)
Check if colors is empty : false
Check if nums is empty : true
```


## Concantenarea Maps

Puteți folosi fie operatorul `++`, fie metoda `Map.++()` pentru a concatena două sau mai multe maps, dar în timp ce adăugați maps, va elimina cheile duplicate.

Încercați următorul exemplu de program pentru a concatena două maps.


```scala
object Demo {
   def main(args: Array[String]) {
      val colors1 = Map("red" -> "#FF0000", "azure" -> "#F0FFFF", "peru" -> "#CD853F")
      val colors2 = Map("blue" -> "#0033FF", "yellow" -> "#FFFF00", "red" -> "#FF0000")

      // use two or more Maps with ++ as operator
      var colors = colors1 ++ colors2
      println( "colors1 ++ colors2 : " + colors )

      // use two maps with ++ as method
      colors = colors1.++(colors2)
      println( "colors1.++(colors2)) : " + colors )
   }
}

output:
colors1 ++ colors2 : Map(blue -> #0033FF, azure -> #F0FFFF, 
   peru -> #CD853F, yellow -> #FFFF00, red -> #FF0000)

colors1.++(colors2)) : Map(blue -> #0033FF, azure -> #F0FFFF, 
   peru -> #CD853F, yellow -> #FFFF00, red -> #FF0000)
```

## Printarea keys si values dintr-un Map

Puteți parcurge cheile și valorile unei hărți folosind loop-ul `„foreach”`. Aici, am folosit metoda `foreach` asociată cu iteratorul pentru a parcurge tastele. În continuare este programul exemplu.

```scala
object Demo {
   def main(args: Array[String]) {
      val colors = Map("red" -> "#FF0000", "azure" -> "#F0FFFF","peru" -> "#CD853F")

      colors.keys.foreach{ i =>  
         print( "Key = " + i )
         println(" Value = " + colors(i) )}
   }
}

output:
Key = red Value = #FF0000
Key = azure Value = #F0FFFF
Key = peru Value = #CD853F
```

## Verificarea daca un key exista in map

Puteți utiliza oricare dintre metodele `Map.contains` pentru a testa dacă o anumită cheie există sau nu pe map. Încercați următorul exemplu de program pentru verificarea tastelor.

```scala
object Demo {
   def main(args: Array[String]) {
      val colors = Map("red" -> "#FF0000", "azure" -> "#F0FFFF", "peru" -> "#CD853F")

      if( colors.contains( "red" )) {
         println("Red key exists with value :"  + colors("red"))
      } else {
           println("Red key does not exist")
      }
      
      if( colors.contains( "maroon" )) {
         println("Maroon key exists with value :"  + colors("maroon"))
      } else {
         println("Maroon key does not exist")
      }
   }
}

output:
Red key exists with value :#FF0000
Maroon key does not exist
```

## Metodele Map

| Sr.No | Metodă                                             | Descriere                                                                                                                                                                            |
|-------|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1     | `def ++(xs: Map[(A, B)]): Map[A, B]`               | Returnează o hartă nouă care conține asocierea dintre această hartă și cea furnizată de xs.                                                                                           |
| 2     | `def -(elem1: A, elem2: A, elems: A*): Map[A, B]`  | Returnează o hartă nouă care conține toate asocierele acestei hărți cu excepția celor cu o cheie egală cu elem1, elem2 sau oricare dintre elems.                                       |
| 3     | `def --(xs: GTO[A]): Map[A, B]`                    | Returnează o hartă nouă cu toate asocierele cheie/valoare ale acestei hărți, cu excepția celor cu o cheie egală cu o cheie din obiectul traversabil xs.                                 |
| 4     | `def get(key: A): Option[B]`                      | Returnează opțional valoarea asociată cu o cheie.                                                                                                                                   |
| 5     | `def iterator: Iterator[(A, B)]`                   | Creează un nou iterator peste toate perechile cheie/valoare ale acestei hărți.                                                                                                        |
| 6     | `def addString(b: StringBuilder): StringBuilder`  | Adaugă toate elementele acestei colecții reduse la un șir de caractere.                                                                                                              |
| 7     | `def addString(b: StringBuilder, sep: String): StringBuilder` | Adaugă toate elementele acestei colecții reduse la un șir de caractere folosind un șir separator specificat.                                                                     |
| 8     | `def apply(key: A): B`                            | Returnează valoarea asociată cu cheia dată sau rezultatul metodei implicite a hărții dacă nu există nicio asociere.                                                               |
| 9     | `def clear(): Unit`                                | Elimină toate legăturile din hartă. După ce această operațiune s-a încheiat, harta va fi goală.                                                                                      |
| 10    | `def clone(): Map[A, B]`                           | Creează o copie a obiectului receptor.                                                                                                                                               |
| 11    | `def contains(key: A): Boolean`                   | Returnează true dacă există o asociere pentru cheia în această hartă, false în caz contrar.                                                                                          |
| 12    | `def copyToArray(xs: Array[(A, B)]): Unit`        | Copiază valorile acestei colecții reduse într-un array. Completează array-ul dat xs cu valorile acestei colecții reduse.                                                          |
| 13    | `def count(p: ((A, B)) => Boolean): Int`          | Numără numărul de elemente din colecția redusă care satisfac o predicție.                                                                                                            |
| 14    | `def default(key: A): B`                          | Definește calculul valorii implicite pentru hartă, returnată atunci când o cheie nu este găsită.                                                                                    |
| 15    | `def drop(n: Int): Map[A, B]`                     | Returnează toate elementele cu excepția primelor n.                                                                                                                                 |
| 16    | `def dropRight(n: Int): Map[A, B]`                | Returnează toate elementele cu excepția ultimelor n.                                                                                                                               |
| 17    | `def dropWhile(p: ((A, B)) => Boolean): Map[A, B]` | Abandonează cel mai lung prefix al elementelor care satisfac o predicție.                                                                                                           |
| 18    | `def empty: Map[A, B]`                             | Returnează harta goală de același tip.                                                                                                                                             |
| 19    | `def equals(that: Any): Boolean`                  | Returnează true dacă ambele hărți conțin exact aceleași chei/valori, false în caz contrar.                                                                                           |
| 20    | `def exists(p: ((A, B)) => Boolean): Boolean`     | Returnează true dacă predicția p este adevărată pentru unele dintre elementele acestei colecții reduse, în caz contrar false.                                                     |
| 21    | `def filter(p: ((A, B))=> Boolean): Map[A, B]`    | Returnează toate elementele acestei colecții reduse care satisfac o predicție.                                                                                                       |
| 22    | `def filterKeys(p: (A) => Boolean): Map[A, B]`    | Returnează o hartă imutabilă formată doar din acele perechi cheie/valoare ale acestei hărți unde cheia satisface predicția p.                                                      |
| 23    | `def find(p: ((A, B)) => Boolean): Option[(A, B)]` | Găsește primul element al colecției reduse care satisface o predicție, dacă există vreunul.                                                                                       |
| 24    | `def foreach(f: ((A, B)) => Unit): Unit`         | Aplică o funcție f tuturor elementelor acestei colecții reduse.                                                                                                                     |
| 25    | `def init: Map[A, B]`                              | Returnează toate elementele cu excepția ultimelor.                                                                                                                                 |
| 26    | `def isEmpty: Boolean`                             | Verifică dacă harta este goală.                                                                                                                                                     |
| 27    | `def keys: Iterable[A]`                            | Returnează un iterator peste toate cheile.                                                                                                                                        |
| 28    | `def last: (A, B)`                                 | Returnează ultimul element.                                                                                                                                                        |
| 29    | `def max: (A, B)`                                  | Găsește cel mai mare element.                                                                                                                                                      |
| 30    | `def min: (A, B)`                                  | Găsește cel mai mic element.                                                                                                                                                       |
| 31    | `def mkString: String`                             | Afișează toate elementele acestei colecții reduse într-un șir de caractere.                                                                                                        |
| 32    | `def product: (A, B)`                              | Returnează produsul tuturor elementelor acestei colecții reduse în ceea ce privește operatorul * în num.                                                                            |
| 33    | `def remove(key: A): Option[B]`                   | Elimină o cheie din această hartă, returnând valoarea asociată anterior cu acea cheie ca opțiune.                                                                                  |
| 34    | `def retain(p: (A, B) => Boolean): Map.this.type` | Menține doar acele asociere pentru care predicția p returnează true.                                                                                                               |
| 35    | `def size: Int`                                    | Returnează numărul de elemente din această hartă.                                                                                                                                  |
| 36    | `def sum: (A, B)`                                  | Returnează suma tuturor elementelor acestei colecții reduse în ceea ce privește operatorul + în num.                                                                              |
| 37    | `def tail: Map[A, B]`                              | Returnează toate elementele cu excepția primelor.                                                                                                                                |
| 38    | `def take(n: Int): Map[A, B]`                      | Returnează primele n elemente.                                                                                                                                                     |
| 39    | `def takeRight(n: Int): Map[A, B]`                 | Returnează ultimele n elemente.                                                                                                                                                    |
| 40    | `def takeWhile(p: ((A, B)) => Boolean): Map[A, B]` | Ia cel mai lung prefix al elementelor care satisfac o predicție.                                                                                                                   |
| 41    | `def toArray: Array[(A, B)]`                       | Convertește această colecție redusă într-un array.                                                                                                                                 |
| 42    | `def toBuffer[B >: A]: Buffer[B]`                 | Returnează un buffer care conține toate elementele acestei hărți.                                                                                                                  |
| 43    | `def toList: List[A]`                              | Returnează o listă care conține toate elementele acestei hărți.                                                                                                                   |
| 44    | `def toSeq: Seq[A]`                                | Returnează o secvență care conține toate elementele acestei hărți.                                                                                                                 |
| 45    | `def toSet: Set[A]`                                | Returnează un set care conține toate elementele acestei hărți.                                                                                                                     |
| 46    | `def toString(): String`                           | Returnează o reprezentare sub formă de șir a obiectului.                                                                                                                           |                             |