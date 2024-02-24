# Scala options

Scala `Option[T] `este un container pentru zero sau un element de un anumit tip. Un obiect `Option[T]` poate fi fie Un `obiect [T]`, fie Nici unul, care reprezintă o valoare lipsă. De exemplu, metoda get a `Map` lui Scala produce `Some(value)` dacă a fost găsită o valoare corespunzătoare unei anumite chei sau `None` dacă cheia dată nu este definită în Map.

Tipul de opțiune este folosit frecvent în programele Scala și îl puteți compara cu valoarea nulă disponibilă în Java, care nu indică nicio valoare. De exemplu, metoda get a lui `java.util.HashMap` returnează fie o valoare stocată în HashMap, fie null dacă nu a fost găsită nicio valoare.

Să presupunem că avem o metodă care preia o înregistrare din baza de date pe baza unei chei primare.

```scala
def findPerson(key: Int): Option[Person]
```

Metoda va returna Some[Person] dacă înregistrarea este găsită, dar None dacă înregistrarea nu este găsită. Să urmăm următorul program.

```scala
object Demo {
   def main(args: Array[String]) {
      val capitals = Map("France" -> "Paris", "Japan" -> "Tokyo")
      
      println("capitals.get( \"France\" ) : " +  capitals.get( "France" ))
      println("capitals.get( \"India\" ) : " +  capitals.get( "India" ))
   }
}

output:
capitals.get( "France" ) : Some(Paris)
capitals.get( "India" ) : None
```

Cel mai obișnuit mod de a demonta valorile opționale este printr-o potrivire a modelului. De exemplu, încercați următorul program.

```scala
object Demo {
   def main(args: Array[String]) {
      val capitals = Map("France" -> "Paris", "Japan" -> "Tokyo")
      
      println("show(capitals.get( \"Japan\")) : " + show(capitals.get( "Japan")) )
      println("show(capitals.get( \"India\")) : " + show(capitals.get( "India")) )
   }
   
   def show(x: Option[String]) = x match {
      case Some(s) => s
      case None => "?"
   }
}

output:
show(capitals.get( "Japan")) : Tokyo
show(capitals.get( "India")) : ?
```

## Utilizarea metodei getOrElse() 

Următorul este exemplul de program pentru a arăta cum să utilizați metoda `getOrElse()` pentru a accesa o valoare sau o valoare implicită atunci când nu este prezentă nicio valoare.

```scala
object Demo {
   def main(args: Array[String]) {
      val a:Option[Int] = Some(5)
      val b:Option[Int] = None 
      
      println("a.getOrElse(0): " + a.getOrElse(0) )
      println("b.getOrElse(10): " + b.getOrElse(10) )
   }
}

output:
a.getOrElse(0): 5
b.getOrElse(10): 10
```

```scala
obiect Demo {
    def main(args: Array[String]) {
       val a:Opțiune[Int] = Unele (5)
       val b:Opțiune[Int] = Nici unul
      
       println("a.isEmpty: " + a.isEmpty )
       println("b.isEmpty: " + b.isEmpty )
    }
}

output:
a.isEmpty: false
b.isEmpty: true
```

## Metodiele Option 

| Sr.No | Metodă                                       | Descriere                                                                                                                                                                                         |
|-------|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1     | `def get: A`                                 | Returnează valoarea opțiunii.                                                                                                                                                                    |
| 2     | `def isEmpty: Boolean`                       | Returnează true dacă opțiunea este None, false în caz contrar.                                                                                                                                    |
| 3     | `def productArity: Int`                      | Dimensiunea acestui produs. Pentru un produs A(x_1, ..., x_k), returnează k.                                                                                                                     |
| 4     | `def productElement(n: Int): Any`            | Al n-lea element al acestui produs, indexat de la 0. Cu alte cuvinte, pentru un produs A(x_1, ..., x_k), returnează x_(n+1) unde 0 < n < k.                                                 |
| 5     | `def exists(p: (A) => Boolean): Boolean`    | Returnează true dacă această opțiune este neagră și predicatul p returnează true când este aplicat pe valoarea acestei opțiuni. În caz contrar, returnează false.                                  |
| 6     | `def filter(p: (A) => Boolean): Option[A]`  | Returnează această opțiune dacă este neagră și aplicarea predicatului p la valoarea acestei opțiuni returnează true. În caz contrar, returnează None.                                        |
| 7     | `def filterNot(p: (A) => Boolean): Option[A]` | Returnează această opțiune dacă este neagră și aplicarea predicatului p la valoarea acestei opțiuni returnează false. În caz contrar, returnează None.                                     |
| 8     | `def flatMap[B](f: (A) => Option[B]): Option[B]` | Returnează rezultatul aplicării f la valoarea acestei opțiuni dacă această opțiune nu este goală. Returnează None dacă această opțiune este goală.                                             |
| 9     | `def foreach[U](f: (A) => U): Unit`          | Aplică procedura dată f valorii opțiunii, dacă aceasta nu este goală. În caz contrar, nu face nimic.                                                                                           |
| 10    | `def getOrElse[B >: A](default: => B): B`    | Returnează valoarea opțiunii dacă opțiunea nu este goală, în caz contrar returnează rezultatul evaluării valorii implicite.                                                                      |
| 11    | `def isDefined: Boolean`                     | Returnează true dacă opțiunea este o instanță Some, false în caz contrar.                                                                                                                        |
| 12    | `def iterator: Iterator[A]`                  | Returnează un iterator singleton care returnează valoarea opțiunii dacă nu este goală, sau un iterator gol dacă opțiunea este goală.                                                         |
| 13    | `def map[B](f: (A) => B): Option[B]`        | Returnează Some conținând rezultatul aplicării f la valoarea acestei opțiuni dacă această opțiune nu este goală. În caz contrar, returnează None.                                             |
| 14    | `def orElse[B >: A](alternative: => Option[B]): Option[B]` | Returnează această opțiune dacă nu este goală, în caz contrar returnează rezultatul evaluării alternativei.                                                                                   |
| 15    | `def orNull`                                 | Returnează valoarea opțiunii dacă nu este goală, sau null dacă este goală.                                                                                                                     |