# Listele in Scala

Listele Scala sunt destul de asemănătoare cu arrays, ceea ce înseamnă că toate elementele unei liste au același tip, dar există două diferențe importante. În primul rând, listele sunt imuabile, ceea ce înseamnă că elementele unei liste nu pot fi modificate prin atribuire. În al doilea rând, listele reprezintă un linked list, în timp ce arrays sunt flat.

Tipul unei liste care are elemente de tip `T` este scris ca `List[T]`.

Încercați următorul exemplu, aici sunt câteva liste definite pentru diferite tipuri de date.

```scala
// List of Strings
val fruit: List[String] = List("apples", "oranges", "pears")

// List of Integers
val nums: List[Int] = List(1, 2, 3, 4)

// Empty List.
val empty: List[Nothing] = List()

// Two dimensional list
val dim: List[List[Int]] =
   List(
      List(1, 0, 0),
      List(0, 1, 0),
      List(0, 0, 1)
   )
```

Toate listele pot fi definite folosind două blocuri fundamentale, o coadă `Nil` și `::`, care se pronunță ``cons. Nil` reprezintă, de asemenea, lista goală. Toate listele de mai sus pot fi definite după cum urmează.

```scala
// List of Strings
val fruit = "apples" :: ("oranges" :: ("pears" :: Nil))

// List of Integers
val nums = 1 :: (2 :: (3 :: (4 :: Nil)))

// Empty List.
val empty = Nil

// Two dimensional list
val dim = (1 :: (0 :: (0 :: Nil))) ::
          (0 :: (1 :: (0 :: Nil))) ::
          (0 :: (0 :: (1 :: Nil))) :: Nil
```

## Operatii basic pe liste

Toate operațiunile pe liste pot fi exprimate în termenii următoarelor trei metode.

| Nr.  | Metodă      | Descriere                                                                                      |
|------|-------------|-----------------------------------------------------------------------------------------------|
| 1    | `head`      | Această metodă returnează primul element al unei liste.                                       |
| 2    | `tail`      | Această metodă returnează o listă formată din toate elementele cu excepția primului.         |
| 3    | `isEmpty`   | Această metodă returnează `true` dacă lista este goală și `false` în caz contrar.             |


```scala
object Demo {
   def main(args: Array[String]) {
      val fruit = "apples" :: ("oranges" :: ("pears" :: Nil))
      val nums = Nil

      println( "Head of fruit : " + fruit.head )
      println( "Tail of fruit : " + fruit.tail )
      println( "Check if fruit is empty : " + fruit.isEmpty )
      println( "Check if nums is empty : " + nums.isEmpty )
   }
}

output:
Head of fruit : apples
Tail of fruit : List(oranges, pears)
Check if fruit is empty : false
Check if nums is empty : true
```

Salvați programul de mai sus în `Demo.scala`. Următoarele comenzi sunt folosite pentru a compila și executa acest program.

## Concatenarea listelor

Puteți utiliza fie operatorul `:::`, fie metoda `List.:::()` sau metoda `List.concat()` pentru a adăuga două sau mai multe liste. Vă rugăm să găsiți următorul exemplu dat mai jos −

```scala
object Demo {
   def main(args: Array[String]) {
      val fruit1 = "apples" :: ("oranges" :: ("pears" :: Nil))
      val fruit2 = "mangoes" :: ("banana" :: Nil)

      // use two or more lists with ::: operator
      var fruit = fruit1 ::: fruit2
      println( "fruit1 ::: fruit2 : " + fruit )
      
      // use two lists with Set.:::() method
      fruit = fruit1.:::(fruit2)
      println( "fruit1.:::(fruit2) : " + fruit )

      // pass two or more lists as arguments
      fruit = List.concat(fruit1, fruit2)
      println( "List.concat(fruit1, fruit2) : " + fruit  )
   }
}

output:
fruit1 ::: fruit2 : List(apples, oranges, pears, mangoes, banana)
fruit1.:::(fruit2) : List(mangoes, banana, apples, oranges, pears)
List.concat(fruit1, fruit2) : List(apples, oranges, pears, mangoes, banana)
```
## Crearea unor liste uniforme

Puteți utiliza metoda `List.fill()` pentru a crea o listă constând din zero sau mai multe copii ale aceluiași element. Încercați următorul exemplu de program.

```scala
object Demo {
   def main(args: Array[String]) {
      val fruit = List.fill(3)("apples") // Repeats apples three times.
      println( "fruit : " + fruit  )

      val num = List.fill(10)(2)         // Repeats 2, 10 times.
      println( "num : " + num  )
   }
}

output:
fruit : List(apples, apples, apples)
num : List(2, 2, 2, 2, 2, 2, 2, 2, 2, 2)
```

## Tabelarea unei functii

Puteți folosi o funcție împreună cu metoda `List.tabulate()` pentru a aplica toate elementele listei înainte de a tabula lista. Argumentele sale sunt la fel ca cele ale `List.fill:` prima listă de argumente oferă dimensiunile listei de creat, iar a doua descrie elementele listei. Singura diferență este că, în loc ca elementele să fie fixe, acestea sunt calculate dintr-o funcție.

Încercați următorul exemplu de program.

```scala
object Demo {
   def main(args: Array[String]) {
      // Creates 5 elements using the given function.
      val squares = List.tabulate(6)(n => n * n)
      println( "squares : " + squares  )

      val mul = List.tabulate( 4,5 )( _ * _ )      
      println( "mul : " + mul  )
   }
}

output:
squares : List(0, 1, 4, 9, 16, 25)
mul : List(List(0, 0, 0, 0, 0), List(0, 1, 2, 3, 4), 
   List(0, 2, 4, 6, 8), List(0, 3, 6, 9, 12))
```

## Reverse List Order

Puteți folosi metoda `List.reverse` pentru a inversa toate elementele listei. Următorul exemplu arată utilizarea.

```scala
object Demo {
   def main(args: Array[String]) {
      val fruit = "apples" :: ("oranges" :: ("pears" :: Nil))
      
      println( "Before reverse fruit : " + fruit )
      println( "After reverse fruit : " + fruit.reverse )
   }
}

output:
Before reverse fruit : List(apples, oranges, pears)
After reverse fruit : List(pears, oranges, apples)
```

## Metodele listelor in scala

| Nr.  | Metodă                                          | Descriere                                                                                                                     |
|------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| 1    | `def +(elem: A): List[A]`                       | Adaugă un element la începutul listei.                                                                                      |
| 2    | `def ::(x: A): List[A]`                          | Adaugă un element la începutul listei.                                                                                      |
| 3    | `def :::(prefix: List[A]): List[A]`              | Adaugă elementele unei liste date în fața acestei liste.                                                                    |
| 4    | `def ::(x: A): List[A]`                          | Adaugă un element la începutul listei.                                                                                      |
| 5    | `def addString(b: StringBuilder): StringBuilder` | Adaugă toate elementele listei la un șir de caractere.                                                                      |
| 6    | `def addString(b: StringBuilder, sep: String): StringBuilder` | Adaugă toate elementele listei la un șir de caractere, utilizând un separator specificat.                             |
| 7    | `def apply(n: Int): A`                           | Selectează un element după index în listă.                                                                                  |
| 8    | `def contains(elem: Any): Boolean`              | Verifică dacă lista conține o anumită valoare ca element.                                                                    |
| 9    | `def copyToArray(xs: Array[A], start: Int, len: Int): Unit` | Copiază elementele listei într-un array. Umple array-ul dat xs cu cel mult length (len) elemente ale acestei liste, începând de la poziția start. |
| 10   | `def distinct: List[A]`                          | Construiește o nouă listă din lista curentă fără elemente duplicate.                                                       |
| 11   | `def drop(n: Int): List[A]`                      | Returnează toate elementele, cu excepția primelor n.                                                                       |
| 12   | `def dropRight(n: Int): List[A]`                 | Returnează toate elementele, cu excepția ultimelor n.                                                                      |
| 13   | `def dropWhile(p: (A) => Boolean): List[A]`      | Elimină cea mai lungă prefixă a elementelor care satisfac o anumită predicție.                                              |
| 14   | `def endsWith[B](that: Seq[B]): Boolean`         | Verifică dacă lista se termină cu secvența dată.                                                                         |
| 15   | `def equals(that: Any): Boolean`                 | Metoda equals pentru secvențe arbitrare. Compară această secvență cu un alt obiect.                                        |
| 16   | `def exists(p: (A) => Boolean): Boolean`        | Verifică dacă o predicție este adevărată pentru unele dintre elementele listei.                                              |
| 17   | `def filter(p: (A) => Boolean): List[A]`        | Returnează toate elementele listei care satisfac o anumită predicție.                                                       |
| 18   | `def forall(p: (A) => Boolean): Boolean`        | Verifică dacă o predicție este adevărată pentru toate elementele listei.                                                     |
| 19   | `def foreach(f: (A) => Unit): Unit`             | Aplică o funcție f tuturor elementelor listei.                                                                            |
| 20   | `def head: A`                                    | Selectează primul element al listei.                                                                                        |
| 21   | `def indexOf(elem: A, from: Int): Int`          | Găsește indexul primei apariții a unei valori în listă, după poziția index dată.                                           |
| 22   | `def init: List[A]`                              | Returnează toate elementele, cu excepția ultimului.                                                                       |
| 23   | `def intersect(that: Seq[A]): List[A]`          | Calculează intersecția multi-seturilor între lista curentă și o altă secvență.                                           |
| 24   | `def isEmpty: Boolean`                           | Verifică dacă lista este goală.                                                                                           |
| 25   | `def iterator: Iterator[A]`                     | Creează un nou iterator peste toate elementele conținute în obiectul iterabil.                                            |
| 26   | `def last: A`                                    | Returnează ultimul element.                                                                                               |
| 27   | `def lastIndexOf(elem: A, end: Int): Int`       | Găsește indexul ultimei apariții a unei valori în listă; înainte sau la un index dat.                                    |
| 28   | `def length: Int`                                 | Returnează lungimea listei.                                                                                              |
| 29   | `def map[B](f: (A) => B): List[B]`              | Construiește o nouă colecție aplicând o funcție tuturor elementelor acestei liste.                                        |
| 30   | `def max: A`                                     | Găsește cel mai mare element.                                                                                             |
| 31   | `def min: A`                                     | Găsește cel mai mic element.                                                                                              |
| 32   | `def mkString: String`                          | Afișează toate elementele listei într-un șir de caractere.                                                                 |
| 33   | `def mkString(sep: String): String`             | Afișează toate elementele listei într-un șir de caractere, utilizând un separator specificat.                             |
| 34   | `def reverse: List[A]`                          | Returnează o nouă listă cu elementele în ordine inversă.                                                                  |
| 35   | `def sorted[B >: A]: List[A]`                   | Ordonează lista în conformitate cu un Ordering dat.                                                                      |
| 36   | `def startsWith[B](that: Seq[B], offset: Int): Boolean` | Verifică dacă lista conține secvența dată la un anumit index.                                                           |
| 37   | `def sum: A`                                    | Adună elementele acestei colecții.                                                                                      |
| 38   | `def tail: List[A]`                              | Returnează toate elementele, cu excepția primului.                                                                      |
| 39   | `def take(n: Int): List[A]`                     | Returnează primele "n

" elemente.                                                                                        |
| 40   | `def takeRight(n: Int): List[A]`                | Returnează ultimele "n" elemente.                                                                                        |
| 41   | `def toArray: Array[A]`                         | Convertește lista într-un array.                                                                                        |
| 42   | `def toBuffer[B >: A]: Buffer[B]`              | Convertește lista într-un buffer mutabil.                                                                               |
| 43   | `def toMap[T, U]: Map[T, U]`                    | Convertește această listă într-un map.                                                                                 |
| 44   | `def toSeq: Seq[A]`                             | Convertește lista într-o secvență.                                                                                     |
| 45   | `def toSet[B >: A]: Set[B]`                     | Convertește lista într-un set.                                                                                         |
| 46   | `def toString(): String`                        | Convertește lista într-un șir de caractere.                                                                            |





