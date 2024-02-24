# Set in Scala

Scala `Set` este o colecție de elemente diferite pe perechi de același tip. Cu alte cuvinte, un set este o colecție care nu conține elemente duplicate. Există două tipuri de seturi, cele `imuabile` și cele `mutabile`. Diferența dintre obiectele mutabile și imuabile este că atunci când un obiect este imuabil, obiectul în sine nu poate fi schimbat.

Implicit, Scala folosește setul imuabil. Dacă doriți să utilizați setul mutabil, va trebui să importați în mod explicit clasa scala.`collection.mutable.Set`. Dacă doriți să utilizați atât seturi mutabile, cât și seturi imuabile în aceeași colecție, atunci puteți continua să vă referiți la Setul imuabil ca Set, dar vă puteți referi la Setul mutabil ca set mutabil.

Iată cum puteți declara seturi imuabile −

```scala
// Empty set of integer type
var s : Set[Int] = Set()

// Set of integer type
var s : Set[Int] = Set(1,3,5,7)

or 

var s = Set(1,3,5,7)
```

În timpul definirii unui set gol, adnotarea tipului este necesară deoarece sistemul trebuie să aloce un tip concret variabilei.

## Operatiuni basic pe Set

| Nr.  | Metodă      | Descriere                                                                                   |
|------|-------------|--------------------------------------------------------------------------------------------|
| 1    | `head`      | Această metodă returnează primul element al unui set.                                      |
| 2    | `tail`      | Această metodă returnează un set format din toate elementele cu excepția primului.        |
| 3    | `isEmpty`   | Această metodă returnează `true` dacă setul este gol și `false` în caz contrar.           |

```scala
object Demo {
   def main(args: Array[String]) {
      val fruit = Set("apples", "oranges", "pears")
      val nums: Set[Int] = Set()

      println( "Head of fruit : " + fruit.head )
      println( "Tail of fruit : " + fruit.tail )
      println( "Check if fruit is empty : " + fruit.isEmpty )
      println( "Check if nums is empty : " + nums.isEmpty )
   }
}

output:
Head of fruit : apples
Tail of fruit : Set(oranges, pears)
Check if fruit is empty : false
Check if nums is empty : true
```

## Concatenarea set-urilor

Puteți folosi fie operatorul `++`, fie metoda `Set.++()` pentru a concatena două sau mai multe seturi, dar în timp ce adăugați seturi, va elimina elementele duplicate.

Următorul este exemplul de concatenare a două seturi.

```scala
object Demo {
   def main(args: Array[String]) {
      val fruit1 = Set("apples", "oranges", "pears")
      val fruit2 = Set("mangoes", "banana")

      // use two or more sets with ++ as operator
      var fruit = fruit1 ++ fruit2
      println( "fruit1 ++ fruit2 : " + fruit )

      // use two sets with ++ as method
      fruit = fruit1.++(fruit2)
      println( "fruit1.++(fruit2) : " + fruit )
   }
}

output:
fruit1 ++ fruit2 : Set(banana, apples, mangoes, pears, oranges)
fruit1.++(fruit2) : Set(banana, apples, mangoes, pears, oranges)
```

## Gasirea Max, Min in Set

Puteți folosi metoda `Set.min` pentru a afla minimul și metoda `Set.max` pentru a afla maximul elementelor disponibile într-un set. Următorul este exemplul pentru a afișa programul.

```scala
object Demo {
   def main(args: Array[String]) {
      val num = Set(5,6,9,20,30,45)

      // find min and max of the elements
      println( "Min element in Set(5,6,9,20,30,45) : " + num.min )
      println( "Max element in Set(5,6,9,20,30,45) : " + num.max )
   }
}

output:
Min element in Set(5,6,9,20,30,45) : 5
Max element in Set(5,6,9,20,30,45) : 45
```

## Gasirea valorilor comune in sets

Puteți utiliza fie metoda `Set.&` sau metoda `Set.intersect` pentru a afla valorile comune între două seturi. Încercați următorul exemplu pentru a arăta utilizarea.

```scala
object Demo {
   def main(args: Array[String]) {
      val num1 = Set(5,6,9,20,30,45)
      val num2 = Set(50,60,9,20,35,55)

      // find common elements between two sets
      println( "num1.&(num2) : " + num1.&(num2) )
      println( "num1.intersect(num2) : " + num1.intersect(num2) )
   }
}

output:
num1.&(num2) : Set(20, 9)
num1.intersect(num2) : Set(20, 9)
```

## Metodele Set in Scala

| Nr.  | Metodă                                           | Descriere                                                                                                                     |
|------|--------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| 1    | `def +(elem: A): Set[A]`                         | Creează un nou set cu un element adițional, cu excepția cazului în care elementul este deja prezent.                       |
| 2    | `def -(elem: A): Set[A]`                         | Creează un nou set cu un element dat eliminat din acest set.                                                                 |
| 3    | `def contains(elem: A): Boolean`                | Returnează `true` dacă elem este conținut în acest set, în caz contrar `false`.                                            |
| 4    | `def &(that: Set[A]): Set[A]`                    | Returnează un nou set format din toate elementele care sunt atât în acest set, cât și în setul dat.                           |
| 5    | `def &~(that: Set[A]): Set[A]`                   | Returnează diferența dintre acest set și alt set.                                                                          |
| 6    | `def +(elem1: A, elem2: A, elems: A*): Set[A]`    | Creează un nou set imutabil cu elemente adiționale din seturile furnizate.                                                   |
| 7    | `def ++(elems: A): Set[A]`                       | Concatenează acest set imutabil cu elementele dintr-o altă colecție în acest set imutabil.                                  |
| 8    | `def -(elem1: A, elem2: A, elems: A*): Set[A]`   | Returnează un nou set imutabil care conține toate elementele din setul imutabil curent, cu excepția unei apariții mai puține a fiecărui element din argumentele date. |
| 9    | `def addString(b: StringBuilder): StringBuilder` | Adaugă toate elementele acestui set imutabil la un șir de caractere.                                                       |
| 10   | `def addString(b: StringBuilder, sep: String): StringBuilder` | Adaugă toate elementele acestui set imutabil la un șir de caractere, utilizând un separator specificat.               |
| 11   | `def apply(elem: A)`                             | Verifică dacă un element este conținut în acest set.                                                                       |
| 12   | `def count(p: (A) => Boolean): Int`             | Numără numărul de elemente din setul imutabil care satisfac o predicție.                                                     |
| 13   | `def copyToArray(xs: Array[A], start: Int, len: Int): Unit` | Copiază elementele acestui set imutabil într-un array. Umple array-ul dat xs cu cel mult length (len) elemente ale acestui set imutabil, începând de la poziția start. |
| 14   | `def diff(that: Set[A]): Set[A]`                | Calculează diferența dintre acest set și un alt set.                                                                      |
| 15   | `def drop(n: Int): Set[A]`                       | Returnează toate elementele, cu excepția primelor n.                                                                       |
| 16   | `def dropRight(n: Int): Set[A]`                  | Returnează toate elementele, cu excepția ultimelor n.                                                                      |
| 17   | `def dropWhile(p: (A) => Boolean): Set[A]`      | Elimină cea mai lungă prefixă a elementelor care satisfac o anumită predicție.                                              |
| 18   | `def equals(that: Any): Boolean`                 | Metoda equals pentru secvențe arbitrare. Compară această secvență cu un alt obiect.                                        |
| 19   | `def exists(p: (A) => Boolean): Boolean`        | Verifică dacă o predicție este adevărată pentru unele dintre elementele acestui set imutabil.                               |
| 20   | `def filter(p: (A) => Boolean): Set[A]`        | Returnează toate elementele acestui set imutabil care satisfac o anumită predicție.                                         |
| 21   | `def find(p: (A) => Boolean): Option[A]`        | Găsește primul element al setului imutabil care satisface o anumită predicție, dacă există.                                |
| 22   | `def forall(p: (A) => Boolean): Boolean`       | Verifică dacă o predicție este adevărată pentru toate elementele acestui set imutabil.                                     |
| 23   | `def foreach(f: (A) => Unit): Unit`             | Aplică o funcție f tuturor elementelor acestui set imutabil.                                                              |
| 24   | `def head: A`                                    | Returnează primul element al acestui set imutabil.                                                                         |
| 25   | `def init: Set[A]`                               | Returnează toate elementele, cu excepția ultimului, ale acestui set imutabil.                                            
| 26   | `def intersect(that: Set[A]): Set[A]`           | Calculează intersecția dintre acest set și un alt set.                                                                     |
| 27   | `def isEmpty: Boolean`                          | Verifică dacă acest set este gol.                                                                                          |
| 28   | `def iterator: Iterator[A]`                     | Creează un nou iterator peste toate elementele conținute în obiectul iterabil.                                           |
| 29   | `def last: A`                                    | Returnează ultimul element.                                                                                                |
| 30   | `def map[B](f: (A) => B): immutable.Set[B]`     | Construiește o nouă colecție aplicând o funcție tuturor elementelor acestui set imutabil.                                  |
| 31   | `def max: A`                                    | Găsește cel mai mare element.                                                                                              |
| 32   | `def min: A`                                    | Găsește cel mai mic element.                                                                                               |
| 33   | `def mkString: String`                          | Afișează toate elementele acestui set imutabil într-un șir de caractere.                                                  |
| 34   | `def mkString(sep: String): String`             | Afișează toate elementele acestui set imutabil într-un șir de caractere folosind un separator specificat.                 |
| 35   | `def product: A`                                | Returnează produsul tuturor elementelor acestui set imutabil în raport cu operatorul * în num.                            |
| 36   | `def size: Int`                                 | Returnează numărul de elemente din acest set imutabil.                                                                     |
| 37   | `def splitAt(n: Int): (Set[A], Set[A])`         | Returnează o pereche de seturi imutabile constând în primele n elemente ale acestui set imutabil și celelalte elemente. |
| 38   | `def subsetOf(that: Set[A]): Boolean`           | Returnează `true` dacă acest set este un submulțime al lui `that`, adică dacă fiecare element al acestui set este, de asemenea, un element al lui `that`. |
| 39   | `def sum: A`                                    | Returnează suma tuturor elementelor acestui set imutabil în raport cu operatorul + în num.                                |
| 40   | `def tail: Set[A]`                               | Returnează un set imutabil constând din toate elementele acestui set imutabil, cu excepția primului.                    |
| 41   | `def take(n: Int): Set[A]`                      | Returnează primele n elemente.                                                                                           |
| 42   | `def takeRight(n: Int): Set[A]`                 | Returnează ultimele n elemente.                                                                                          |
| 43   | `def toArray: Array[A]`                         | Returnează un array care conține toate elementele acestui set imutabil.                                                  |
| 44   | `def toBuffer[B >: A]: Buffer[B]`               | Returnează un buffer care conține toate elementele acestui set imutabil.                                                |
| 45   | `def toList: List[A]`                            | Returnează o listă care conține toate elementele acestui set imutabil.                                                  |
| 46   | `def toMap[T, U]: Map[T, U]`                     | Convertește acest set imutabil într-un map.                                                                            |
| 47   | `def toSeq: Seq[A]`                              | Returnează o secvență care conține toate elementele acestui set imutabil.                                              |
| 48   | `def toString(): String`                        | Returnează o reprezentare String a obiectului.                                                                         |

