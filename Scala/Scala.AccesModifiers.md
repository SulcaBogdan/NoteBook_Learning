# Acces Modifiers in Scala

Acest capitol vă prezintă modificatorii de acces Scala. Membrii pachetelor, claselor sau obiectelor pot fi etichetați cu modificatorii de acces private și protejate, iar dacă nu folosim niciunul dintre aceste două cuvinte cheie, atunci accesul va fi considerat public. Acești modificatori restricționează accesul membrilor la anumite regiuni de cod. Pentru a utiliza un modificator de acces, includeți cuvântul său cheie în definiția membrilor pachetului, clasei sau obiectului, așa cum vom vedea în secțiunea următoare.

## Membrii privați
Un membru privat este vizibil numai în interiorul clasei sau al obiectului care conține definiția membrului.

Următorul este exemplul de fragment de cod pentru a explica Private Member −

```scala
class Outer {
   class Inner {
      private def f() { println("f") }
      
      class InnerMost {
         f() // OK
      }
   }
   (new Inner).f() // Error: f is not accessible
}
```

La Scala, accesul (nou `Inner`). `f()` este ilegal deoarece `f` este declarat privat în `Inner` și accesul nu este din clasa `Inner`. Prin contrast, primul acces la `f` din clasa `Innermost` este OK, deoarece acel acces este conținut în corpul clasei `Inner`. Java ar permite ambele accesări, deoarece permite unei clase exterioare să acceseze membrii privați ai claselor sale interioare.

## Membrii protejați
Un membru protejat este accesibil numai din subclasele clasei în care este definit membrul.

Următorul este exemplul de fragment de cod pentru a explica membrul protejat −

```scala
package p {
   class Super {
      protected def f() { println("f") }
   }
   
   class Sub extends Super {
      f()
   }
   
   class Other {
      (new Super).f() // Error: f is not accessible
   }
}
```

Accesul la `f` în clasa Sub este OK deoarece `f` este declarat protejat în clasa `„Super”`, iar clasa `„Sub”` este o subclasă a Super. În schimb, accesul la `f` în clasa `„Alt”` nu este permis, deoarece clasa „Altul” nu moștenește din clasa „Super”. În Java, accesul din urmă ar fi încă permis deoarece clasa `„Alt”` este în același pachet cu clasa `„Sub”`.

## Membrii publici
Spre deosebire de membrii `privați` și `protejați`, nu este necesar să specificați cuvântul cheie `Public` pentru membrii publici. Nu există niciun modificator explicit pentru membrii publici. Astfel de membri pot fi accesați de oriunde.

Următorul este exemplul de fragment de cod pentru a explica membrul public −

```scala
class Outer {
   class Inner {
      def f() { println("f") }
      
      class InnerMost {
         f() // OK
      }
   }
   (new Inner).f() // OK because now f() is public
}
```
## Scope of Protection
Modificatorii de acces în Scala pot fi măriți cu calificative. Un modificator al formei `private[X]` sau `protected[X]` înseamnă că accesul este privat sau protejat `„până la” X`, unde `X` desemnează un pachet, o clasă sau un obiect singleton.

Luați în considerare următorul exemplu −

```scala
package society {
   package professional {
      class Executive {
         private[professional] var workDetails = null
         private[society] var friends = null
         private[this] var secrets = null

         def help(another : Executive) {
            println(another.workDetails)
            println(another.secrets) //ERROR
         }
      }
   }
}
```

- Variabila `workDetails` va fi accesibila oricărei clase din pachetul `profesional` alăturat.

- Variabila `friends` va fi accesibila oricărei clase din cadrul societății de pachete incluse.

- Variabila `secrets` vor fi accesibile numai pe obiectul implicit din cadrul metodelor de instanță (aceasta).