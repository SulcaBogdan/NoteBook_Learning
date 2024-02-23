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

## Operatii basin pe liste

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



