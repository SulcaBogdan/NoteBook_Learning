# Arrays in Scala

Scala oferă o structură de date, `array`, care stochează o colecție secvențială de dimensiuni fixe de elemente de același tip. Un array este folosită pentru a stoca o colecție de date, dar este adesea mai util să ne gândim la o array ca la o colecție de variabile de același tip.

În loc să declarați variabile individuale, cum ar fi `number0`, `number1`, ... și `number99`, declarați o variabilă `array`, cum ar fi numere și utilizați `numere[0], numere[1] și ..., numere[99]` pentru a reprezenta variabile individuale. 

## Declararea unui Array in Scala

Pentru a utiliza un array într-un program, trebuie să declarați o variabilă care să facă referire la array și trebuie să specificați tipul de array la care poate face referire variabila.

Următoarea este sintaxa pentru declararea unei variabile array.

```scala
var z:Array[String] = new Array[String](3)

or

var z = new Array[String](3)
```
Aici, z este declarat ca un array de String-uri care poate conține până la trei elemente. Valorile pot fi atribuite elementelor individuale sau pot avea acces la elemente individuale, se poate face folosind comenzi precum următoarele -

```scala
z(0) = "Zara"; z(1) = "Nuha"; z(4/2) = "Ayan"
```

Aici, ultimul exemplu arată că, în general, indicele poate fi orice expresie care dă un număr întreg. Mai există o modalitate de a defini un array -

```scala
var z = Array("Zara", "Nuha", "Ayan")
```

Imaginea următoare reprezintă un array `myList`. Aici, `myList` conține zece valori duble, iar indicii sunt de la 0 la 9.

![img](https://www.tutorialspoint.com/scala/images/java_array.jpg)

## Procesarea Arrays

Când procesăm elemente din array, folosim adesea structuri de control în loop, deoarece toate elementele dintr-o array sunt de același tip și dimensiunea array-ului este cunoscută.

Mai jos este un exemplu de program care arată cum să creați, să inițializați și să procesați array -

```scala
object Demo {
   def main(args: Array[String]) {
      var myList = Array(1.9, 2.9, 3.4, 3.5)
      
      // Print all the array elements
      for ( x <- myList ) {
         println( x )
      }

      // Summing all elements
      var total = 0.0;
      
      for ( i <- 0 to (myList.length - 1)) {
         total += myList(i);
      }
      println("Total is " + total);

      // Finding the largest element
      var max = myList(0);
      
      for ( i <- 1 to (myList.length - 1) ) {
         if (myList(i) > max) max = myList(i);
      }
      
      println("Max is " + max);
   }
}

output:
1.9
2.9
3.4
3.5
Total is 11.7
Max is 3.5
```

Scala nu acceptă direct diverse operații de array și oferă diverse metode de procesare a matricelor în orice dimensiune. Dacă doriți să utilizați diferite metode, atunci este necesar să importați pachetul `Array._.`

## Array-urile multi-dimensionale

Există multe situații în care ar trebui să definiți și să utilizați arrays multidimensionale (adică array ale căror elemente sunt array). De exemplu, matricele și tabelele sunt exemple de structuri care pot fi realizate ca tablouri bidimensionale.

Următorul este un exemplu de definire a unui tablou bidimensional −

```scala
var myMatrix = ofDim[Int](3,3)
```

Aceasta este un array care are trei elemente fiecare fiind o array de numere întregi care are trei elemente.

Încercați următorul exemplu de program pentru a procesa o array multidimensională -

```scala
import Array._

object Demo {
   def main(args: Array[String]) {
      var myMatrix = ofDim[Int](3,3)
      
      // build a matrix
      for (i <- 0 to 2) {
         for ( j <- 0 to 2) {
            myMatrix(i)(j) = j;
         }
      }
      
      // Print two dimensional array
      for (i <- 0 to 2) {
         for ( j <- 0 to 2) {
            print(" " + myMatrix(i)(j));
         }
         println();
      }
   }
}

output:
0 1 2
0 1 2
0 1 2
```

## Concatenarea arrays

Încercați următorul exemplu care folosește metoda `concat()` pentru a concatena două array. Puteți trece mai mult de o array ca argumente metodei `concat()`.

```scala
import Array._

object Demo {
   def main(args: Array[String]) {
      var myList1 = Array(1.9, 2.9, 3.4, 3.5)
      var myList2 = Array(8.9, 7.9, 0.4, 1.5)

      var myList3 =  concat( myList1, myList2)
      
      // Print all the array elements
      for ( x <- myList3 ) {
         println( x )
      }
   }
}

output:
1.9
2.9
3.4
3.5
8.9
7.9
0.4
1.5
```

## Crearea unui array cu Range
Utilizarea metodei range() pentru a genera un array care conține o secvență de numere întregi crescătoare într-un interval dat. Puteți folosi argumentul final ca pas pentru a crea secvența; dacă nu utilizați argumentul final, atunci pasul ar fi presupus ca 1.

Să luăm un exemplu de creare a unei array de interval (10, 20, 2): înseamnă crearea unei array cu elemente între 10 și 20 și diferența de interval 2. Elementele din array sunt 10, 12, 14, 16 și 18 .

Un alt exemplu: interval (10, 20). Aici diferența de interval nu este dată, așa că implicit presupune 1 element. Se creează o array cu elemente între 10 și 20 cu diferența de interval 1. Elementele din array sunt 10, 11, 12, 13, … și 19.

Următorul exemplu de program arată cum să creați o array cu intervale.

```scala
import Array._

object Demo {
   def main(args: Array[String]) {
      var myList1 = range(10, 20, 2)
      var myList2 = range(10,20)

      // Print all the array elements
      for ( x <- myList1 ) {
         print( " " + x )
      }
      
      println()
      for ( x <- myList2 ) {
         print( " " + x )
      }
   }
}

output:
10 12 14 16 18
10 11 12 13 14 15 16 17 18 19
```

## Metodele Arrays in Scala

Mai jos sunt metodele importante, pe care le puteți folosi în timp ce vă jucați cu array. După cum se arată mai sus, ar trebui să importați pachetul `Array._` înainte de a utiliza oricare dintre metodele menționate. Pentru o listă completă a metodelor disponibile, vă rugăm să verificați documentația oficială Scala

| Nr.  | Metodă                                                                                                       | Descriere                                                                                                      |
|------|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| 1    | `def apply( x: T, xs: T* ): Array[T]`                                                                      | Creează un array de obiecte de tipul T, unde T poate fi Unit, Double, Float, Long, Int, Char, Short, Byte, Boolean. |
| 2    | `def concat[T]( xss: Array[T]* ): Array[T]`                                                               | Concatenează toate array-urile într-un singur array.                                                            |
| 3    | `def copy( src: AnyRef, srcPos: Int, dest: AnyRef, destPos: Int, length: Int ): Unit`                        | Copiază un array în altul. Echivalent cu System.arraycopy(src, srcPos, dest, destPos, length) în Java.         |
| 4    | `def empty[T]: Array[T]`                                                                                   | Returnează un array de lungime 0.                                                                              |
| 5    | `def iterate[T]( start: T, len: Int )( f: (T) => T ): Array[T]`                                            | Returnează un array conținând aplicații repetate ale unei funcții asupra unei valori de start.                |
| 6    | `def fill[T]( n: Int )(elem: => T): Array[T]`                                                             | Returnează un array care conține rezultatele unei computații de elemente de un anumit număr de ori.           |
| 7    | `def fill[T]( n1: Int, n2: Int )( elem: => T ): Array[Array[T]]`                                          | Returnează un array bidimensional care conține rezultatele unei computații de elemente de un anumit număr de ori. |
| 8    | `def iterate[T]( start: T, len: Int)( f: (T) => T ): Array[T]`                                            | Returnează un array conținând aplicații repetate ale unei funcții asupra unei valori de start.                |
| 9    | `def ofDim[T]( n1: Int ): Array[T]`                                                                        | Creează un array cu dimensiunea specificată.                                                                    |
| 10   | `def ofDim[T]( n1: Int, n2: Int ): Array[Array[T]]`                                                        | Creează un array bidimensional.                                                                                |
| 11   | `def ofDim[T]( n1: Int, n2: Int, n3: Int ): Array[Array[Array[T]]]`                                       | Creează un array tridimensional.                                                                              |
| 12   | `def range( start: Int, end: Int, step: Int ): Array[Int]`                                                | Returnează un array conținând valori spațiate în mod egal într-un interval de numere întregi.                |
| 13   | `def range( start: Int, end: Int ): Array[Int]`                                                            | Returnează un array conținând o secvență de numere întregi crescătoare într-un interval.                       |
| 14   | `def tabulate[T]( n: Int )(f: (Int)=> T): Array[T]`                                                       | Returnează un array conținând valorile unei funcții date peste o gamă de valori întregi, începând de la 0.     |
| 15   | `def tabulate[T]( n1: Int, n2: Int )( f: (Int, Int ) => T): Array[Array[T]]`                              | Returnează un array bidimensional conținând valorile unei funcții date peste intervale de valori întregi, începând de la 0. |
****