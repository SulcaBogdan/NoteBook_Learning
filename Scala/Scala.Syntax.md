# Sintaxa in Scala

Dacă ai o înțelegere bună a limbajului Java, atunci va fi foarte ușor pentru tine să înveți Scala. Cea mai mare diferență sintactică între Scala și Java constă în faptul că caracterul de sfârșit de linie ';' este opțional.

Atunci când analizăm un program Scala, acesta poate fi definit ca o colecție de obiecte care comunică prin invocarea metodelor fiecărui obiect. Să aruncăm acum o privire scurtă asupra semnificației claselor, obiectelor, metodelor și variabilelor de instanță.

- **Obiect** − Obiectele au stări și comportamente. Un obiect este o instanță a unei clase. Exemplu − Un câine are stări - culoare, nume, rasă, precum și comportamente - mângâiere, lătrat și mâncare.

- **Clasă** − O clasă poate fi definită ca un șablon/plan care descrie comportamentele/stările care sunt legate de clasa respectivă.

- **Metode** − O metodă este în principal un comportament. O clasă poate conține multe metode. In metode se scriu logici, se manipulează datele și se execută toate acțiunile.

- **Câmpuri** − Fiecare obiect are propria sa serie unică de variabile de instanță, numite câmpuri. Starea unui obiect este creată de valorile atribuite acestor câmpuri.

- **Închidere (Closure)** − O închidere este o funcție ale cărei valoare de returnare depinde de valoarea unei sau mai multor variabile declarate în afara acestei funcții.

- **Atribute (Traits)** − Un atribut încapsulează definiții de metode și câmpuri, care pot fi apoi reutilizate prin amestecarea lor în clase. Atributele sunt folosite pentru a defini tipuri de obiecte prin specificarea semnăturii metodelor suportate.

## Sintaxa de bază
Următoarele sunt sintaxele de bază și convențiile de codare în programarea Scala.


- `Sensibilitate la majuscule și minuscule` - Scala face distincție între majuscule și minuscule, ceea ce înseamnă că identificatorul hello și Hello ar avea semnificații diferite în Scala.

- `Nume de clasă` - Pentru toate numele de clasă, prima literă trebuie să fie cu majuscule. Dacă sunt folosite mai multe cuvinte pentru a forma un nume al clasei, prima literă a fiecărui cuvânt interior trebuie să fie cu majuscule.

`Exemplu − clasa MyFirstScalaClass.`

- `Numele metodelor` - Toate numele metodelor ar trebui să înceapă cu o literă minusculă. Dacă sunt folosite mai multe cuvinte pentru a forma numele metodei, atunci prima literă a fiecărui cuvânt interior ar trebui să fie cu majuscule.

`Exemplu - def myMethodName()`

- `Nume fișier program` - Numele fișierului program trebuie să se potrivească exact cu numele obiectului. Când salvați fișierul, ar trebui să îl salvați folosind numele obiectului (rețineți că Scala face distincție între majuscule și minuscule) și să adăugați „.scala” la sfârșitul numelui. (Dacă numele fișierului și numele obiectului nu se potrivesc, programul dvs. nu se va compila).

`Exemplu − Să presupunem că „HelloWorld” este numele obiectului. Apoi fișierul ar trebui salvat ca „HelloWorld.scala”.`

- `def main(args: Array[String])` − Procesarea programului Scala începe de la metoda main() care este o parte obligatorie a fiecărui program Scala.

## Linii goale și spațiu alb
O linie care conține doar spații albe, eventual cu un comentariu, este cunoscută ca o linie goală, iar Scala o ignoră total. Jetoanele pot fi separate prin spații albe și/sau comentarii.

## Personaje Newline
Scala este un limbaj orientat pe linii în care instrucțiunile pot fi terminate cu punct și virgulă (;) sau linii noi. Un punct și virgulă la sfârșitul unei instrucțiuni este de obicei opțional. Puteți introduce unul dacă doriți, dar nu este necesar dacă declarația apare de la sine pe o singură linie. Pe de altă parte, un punct și virgulă este necesar dacă scrieți mai multe instrucțiuni pe o singură linie. Sub sintaxă este utilizarea mai multor instrucțiuni.

```scala
val s = "hello"; println(s)
```

## Scala packages

Un pachet este un modul de cod numit. De exemplu, pachetul de utilitate `Lift` este `net.liftweb.util`. Declarația pachetului este prima linie fără comentarii din fișierul sursă, după cum urmează -

```scala
package com.liftcode.stuff
```

Pachetele Scala pot fi importate astfel încât să poată fi referite în domeniul actual de compilare. Următoarea instrucțiune importă conținutul pachetului scala.xml −

```scala
import scala.xml._
```

Puteți importa o singură clasă și obiect, de exemplu, HashMap din pachetul scala.collection.mutable -

```scala
import scala.collection.mutable.HashMap
```

Puteți importa mai multe clase sau obiecte dintr-un singur pachet, de exemplu, TreeMap și TreeSet din pachetul scala.collection.immutable -

```scala
import scala.collection.immutable.{TreeMap, TreeSet}
```


## Apply Dynamic
O trăsătură de marcare care permite invocări dinamice. Instanțele x ale acestei trăsături permit invocarea metodei x.meth(args) pentru nume de metode arbitrare meth și liste de argumente args, precum și accesări la câmp x.field pentru nume de câmp arbitrar. Această caracteristică este introdusă în Scala-2.10.

Dacă un apel nu este suportat nativ de x (adică dacă verificarea tipului eșuează), este rescris conform următoarelor reguli -

```scala
foo.method("blah") ~~> foo.applyDynamic("method")("blah")
foo.method(x = "blah") ~~> foo.applyDynamicNamed("method")(("x", "blah"))
foo.method(x = 1, 2) ~~> foo.applyDynamicNamed("method")(("x", 1), ("", 2))
foo.field ~~> foo.selectDynamic("field")
foo.varia = 10 ~~> foo.updateDynamic("varia")(10)
foo.arr(10) = 13 ~~> foo.selectDynamic("arr").update(10, 13)
foo.arr(10) ~~> foo.applyDynamic("arr")(10)
```