# Loops in Scala

Acest capitol vă prezintă structurile de control al loops din limbajele de programare Scala.

Poate exista o situație în care trebuie să executați un bloc de cod de mai multe ori. În general, instrucțiunile sunt executate secvențial: prima instrucțiune dintr-o funcție este executată prima, urmată de a doua și așa mai departe.

Limbajele de programare oferă diverse structuri de control care permit căi de execuție mai complicate.

O instrucțiune buclă ne permite să executăm o instrucțiune sau un grup de instrucțiuni de mai multe ori, iar următoarea este forma generală a unei instrucțiuni buclă în majoritatea limbajelor de programare -

![img](https://www.tutorialspoint.com/scala/images/loop_architecture.jpg)

Limbajul de programare Scala oferă următoarele tipuri de loops pentru a gestiona cerințele de loop:

| Sr.No | Tipul de Bucle      | Descriere                                                                                           |
|-------|---------------------|-----------------------------------------------------------------------------------------------------|
| 1     | `while loop`          | Repetă o instrucțiune sau un grup de instrucțiuni atâta timp cât o anumită condiție este adevărată. Testează condiția înainte de a executa corpul buclei. |
| 2     | `do-while loop`       | Similar cu instrucțiunea while, cu excepția faptului că testează condiția la sfârșitul corpului buclei. |
| 3     | `for loop`            | Execută o secvență de instrucțiuni de mai multe ori și abreviază codul care gestionează variabila de buclă. |

## while loop

Repetă o declarație sau un grup de afirmații în timp ce o anumită condiție este `adevărată`. Testează condiția înainte de a executa corpul buclei. O instrucțiune de buclă while execută în mod repetat o instrucțiune țintă atâta timp cât o anumită condiție este adevărată.

Sintaxa:

```scala
while(condition){
   statement(s);
}
```

Aici, declarațiile pot fi o singură declarație sau un bloc de declarații. Condiția poate fi orice expresie și adevărat este orice valoare diferită de zero. Loop-ul se repetă în timp ce condiția este adevărată. Când condiția devine falsă, controlul programului trece la linia imediat următoare buclei.

![img](https://www.tutorialspoint.com/scala/images/scala_while_loop.jpg)

Aici, punctul cheie al buclei while este că bucla s-ar putea să nu ruleze niciodată. Când condiția este testată și rezultatul este fals, corpul buclei va fi omis și prima instrucțiune după bucla while va fi executată.

Încercați următorul exemplu de program pentru a înțelege instrucțiunile de control al buclei (instrucțiunea while) în limbajul de programare Scala.

```scala
object Demo {
   def main(args: Array[String]) {
      // Local variable declaration:
      var a = 10;

      // while loop execution
      while( a < 20 ){
         println( "Value of a: " + a );
         a = a + 1;
      }
   }
}

output:
value of a: 10
value of a: 11
value of a: 12
value of a: 13
value of a: 14
value of a: 15
value of a: 16
value of a: 17
value of a: 18
value of a: 19
```

## do-while loop

Spre deosebire de bucla while, care testează starea buclei în partea de sus a buclei, bucla do-while își verifică starea în partea de jos a buclei. O buclă do-while este similară cu o buclă while, cu excepția faptului că o buclă do-while este garantată să se execute cel puțin o dată.

Sintaxa:
```scala
do {
   statement(s);
} 
while( condition );
```
Observați că expresia condiționată apare la sfârșitul buclei, astfel încât instrucțiunile din buclă se execută o dată înainte ca condiția să fie testată. Dacă condiția este adevărată, fluxul de control sare înapoi pentru a face și instrucțiunile din buclă se execută din nou. Acest proces se repetă până când condiția dată devine falsă.

![img](https://www.tutorialspoint.com/scala/images/scala_do_while_loop.jpg)

```scala
object Demo {
   def main(args: Array[String]) {
      // Local variable declaration:
      var a = 10;

      // do loop execution
      do {
         println( "Value of a: " + a );
         a = a + 1;
      }
      while( a < 20 )
   }
}

output:
value of a: 10
value of a: 11
value of a: 12
value of a: 13
value of a: 14
value of a: 15
value of a: 16
value of a: 17
value of a: 18
value of a: 19
```

## for loop

O `buclă for` este o structură de control al repetiției care vă permite să scrieți eficient o buclă care trebuie să fie executată de un anumit număr de ori. Există diferite forme de `buclă for` în Scala, care sunt descrise mai jos -

Sintaxa

```scala
for( var x <- Range ){
   statement(s);
}
```

Aici, Intervalul poate fi un interval de numere și care este reprezentat ca de la `i` la `j` sau cândva ca de la `i` până la `j`. Operatorul săgeată la stânga `←` este numit `generator`, numit astfel deoarece generează valori individuale dintr-un interval.

Încercați următorul exemplu de program pentru a înțelege instrucțiunile de control al buclei (pentru instrucțiune) în limbajul de programare Scala.

```scala
object Demo {
   def main(args: Array[String]) {
      var a = 0;
      
      // for loop execution with a range
      for( a <- 1 to 10){
         println( "Value of a: " + a );
      }
   }
}

output:
value of a: 1
value of a: 2
value of a: 3
value of a: 4
value of a: 5
value of a: 6
value of a: 7
value of a: 8
value of a: 9
value of a: 10
```

Puteți utiliza mai multe intervale separate prin punct și virgulă `(;)` în bucla for și, în acest caz, bucla va itera prin toate calculele posibile ale intervalelor date. Următorul este un exemplu de utilizare a doar două intervale, puteți utiliza și mai mult de două intervale.

```scala
object Demo {
   def main(args: Array[String]) {
      var a = 0;
      var b = 0;
      
      // for loop execution with a range
      for( a <- 1 to 3; b <- 1 to 3){
         println( "Value of a: " + a );
         println( "Value of b: " + b );
      }
   }
}

output:
Value of a: 1
Value of b: 1
Value of a: 1
Value of b: 2
Value of a: 1
Value of b: 3
Value of a: 2
Value of b: 1
Value of a: 2
Value of b: 2
Value of a: 2
Value of b: 3
Value of a: 3
Value of b: 1
Value of a: 3
Value of b: 2
Value of a: 3
Value of b: 3
```

### Sintaxa for loop cu Collections

```scala
for( var x <- List ){
   statement(s);
}
```
Aici, variabila Listă este un tip de colecție care are o listă de elemente și se repetă în buclă prin toate elementele care returnează câte un element în variabila x la un moment dat.

Încercați următorul exemplu de program pentru a înțelege bucla cu o colecție de numere. Aici am creat această colecție folosind List(). Vom studia colecțiile într-un capitol separat. Instrucțiuni de control al buclei (pentru instrucțiune) în limbajul de programare Scala.

```scala
object Demo {
   def main(args: Array[String]) {
      var a = 0;
      val numList = List(1,2,3,4,5,6);

      // for loop execution with a collection
      for( a <- numList ){
         println( "Value of a: " + a );
      }
   }
}

output:
value of a: 1
value of a: 2
value of a: 3
value of a: 4
value of a: 5
value of a: 6
```

### Sintaxa for loop cu Filters

Bucla for a lui Scala permite filtrarea unor elemente folosind una sau mai multe declarații if. Mai jos este sintaxa buclei for împreună cu filtrele. Pentru a adăuga mai mult de un filtru la o expresie `for`, separați filtrele cu punct și virgulă (;).


```scala
for( var x <- List
      if condition1; if condition2...
   ){
   statement(s);
}
```

```scala
object Demo {
   def main(args: Array[String]) {
      var a = 0;
      val numList = List(1,2,3,4,5,6,7,8,9,10);

      // for loop execution with multiple filters
      for( a <- numList
           if a != 3; if a < 8 ){
         println( "Value of a: " + a );
      }
   }
}

output:
value of a: 1
value of a: 2
value of a: 4
value of a: 5
value of a: 6
value of a: 7
```

### Sintaxa for loop cu yield

Puteți stoca valorile returnate dintr-o buclă „for” într-o variabilă sau puteți reveni printr-o funcție. Pentru a face acest lucru, prefixați corpul expresiei „pentru” cu cuvântul cheie `yield`. Următoarea este sintaxa.

```scala
var retVal = for{ var x <- List
   if condition1; if condition2...
}
yield x
```

Notă − acoladele au fost folosite pentru a păstra variabilele și condițiile, iar `retVal` este o variabilă în care toate valorile lui `x` vor fi stocate sub formă de colecție.

Încercați următorul exemplu de program pentru a înțelege bucla cu yield.

```scala
object Demo {
   def main(args: Array[String]) {
      var a = 0;
      val numList = List(1,2,3,4,5,6,7,8,9,10);

      // for loop execution with a yield
      var retVal = for{ a <- numList if a != 3; if a < 8 }yield a

      // Now print returned values using another loop.
      for( a <- retVal){
         println( "Value of a: " + a );
      }
   }
}

output:
value of a: 1
value of a: 2
value of a: 4
value of a: 5
value of a: 6
value of a: 7
```

## Loop control statement

Instrucțiunile de control al buclei modifică execuția din secvența normală. Când execuția părăsește un domeniu, toate obiectele automate care au fost create în acel domeniu sunt distruse. Ca atare, Scala nu acceptă declarația `break` sau `continue` așa cum o face Java, dar începând cu versiunea Scala 2.8, există o modalitate de a întrerupe buclele. 

| Sr.No | Declarație de Control | Descriere                                                                                           |
|-------|------------------------|-----------------------------------------------------------------------------------------------------|
| 1     | `break statement`        | Termină instrucțiunea de buclă și transferă execuția la instrucțiunea imediat următoare buclei.    |

Ca atare, nu există nicio instrucțiune `break` încorporată disponibilă în Scala, dar dacă rulați Scala versiunea 2.8, atunci există o modalitate de a utiliza instrucțiunea `break`. Când instrucțiunea `break` este întâlnită în interiorul unei bucle, bucla este imediat încheiată și controlul programului se reia la următoarea instrucțiune care urmează buclei.

![img](https://www.tutorialspoint.com/scala/images/scala_break_statement.jpg)

Sintaxa:

```scala
// import following package
import scala.util.control._

// create a Breaks object as follows
val loop = new Breaks;

// Keep the loop inside breakable as follows
loop.breakable {
   // Loop will go here
   for(...){
      ....
      
      // Break will go here
      loop.break;
   }
}
```

```scala
import scala.util.control._

object Demo {
   def main(args: Array[String]) {
      var a = 0;
      val numList = List(1,2,3,4,5,6,7,8,9,10);

      val loop = new Breaks;
      
      loop.breakable {
         for( a <- numList){
            println( "Value of a: " + a );
            
            if( a == 4 ){
               loop.break;
            }
         }
      }
      println( "After the loop" );
   }
}

output:
Value of a: 1
Value of a: 2
Value of a: 3
Value of a: 4
After the loop
```

## Breaking Nested Loops

Pauza existentă are o problemă în timpul utilizării pentru bucle nested. Doar în cazul în care folosiți `break` pentru bucle nested, urmați această metodă. Acesta este un exemplu de program pentru întreruperea buclelor nested.

```scala
import scala.util.control._

object Demo {
   def main(args: Array[String]) {
      var a = 0;
      var b = 0;
      val numList1 = List(1,2,3,4,5);
      val numList2 = List(11,12,13);

      val outer = new Breaks;
      val inner = new Breaks;

      outer.breakable {
         for( a <- numList1){
            println( "Value of a: " + a );
            
            inner.breakable {
               for( b <- numList2){
                  println( "Value of b: " + b );
                  
                  if( b == 12 ){
                     inner.break;
                  }
               }
            } // inner breakable
         }
      } // outer breakable.
   }
}

output:
Value of a: 1
Value of b: 11
Value of b: 12
Value of a: 2
Value of b: 11
Value of b: 12
Value of a: 3
Value of b: 11
Value of b: 12
Value of a: 4
Value of b: 11
Value of b: 12
Value of a: 5
Value of b: 11
Value of b: 12
```

## The infinite loop

O buclă devine o buclă infinită dacă o condiție nu devine niciodată falsă. Dacă utilizați Scala, bucla while este cea mai bună modalitate de a implementa bucla infinită.

Următorul program implementează bucla infinită.

```scala
object Demo {
   def main(args: Array[String]) {
      var a = 10;
      
      // An infinite loop.
      while( true ){
         println( "Value of a: " + a );
      }
   }
}

output:
Value of a: 10
Value of a: 10
Value of a: 10
Value of a: 10
…………….
```