# Strings in Scala

În Scala, ca și în Java, un string este un obiect `imutabil`, adică un obiect care nu poate fi modificat. Pe de altă parte, obiectele care pot fi modificate, cum ar fi matricele, sunt numite obiecte mutabile. String-urile sunt obiecte foarte utile, în restul acestei secțiuni, vă prezentăm metode importante ale clasei j**ava.lang.String**.

## Crearea unui string

```scala
var greeting = "Hello world!";

or

var greeting: String = "Hello world!";
```
Ori de câte ori compilatorul întâlnește un String literal în cod, acesta creează un obiect String cu valoarea sa, în acest caz, „`Hello world!`”. Cuvântul cheie String poate fi dat și în declarație alternativă, așa cum se arată mai sus.

Încercați următorul exemplu de program.

```scala
object Demo {
   val greeting: String = "Hello, world!"

   def main(args: Array[String]) {
      println( greeting )
   }
}

output:
Hello, world!
```

După cum am menționat mai devreme, clasa String este imuabilă. Obiectul String odată creat nu poate fi modificat. Dacă este necesar să faceți o mulțime de modificări la șirurile de caractere, atunci utilizați Clasa `String Builder` disponibilă în Scala!.

## Lungimea unui String

Metodele folosite pentru a obține informații despre un obiect sunt cunoscute ca metode accesorii. O metodă de accesare care poate fi utilizată cu șiruri de caractere este metoda `length()`, care returnează numărul de caractere conținut în obiectul string.

Utilizați următorul segment de cod pentru a găsi lungimea unui string -

```scala
object Demo {
   def main(args: Array[String]) {
      var palindrome = "Dot saw I was Tod";
      var len = palindrome.length();
      
      println( "String Length is : " + len );
   }
}

output:
String Length is : 17
```

## Concatenarea string-urilor

Clasa String include o metodă de concatenare a două string-uri -

```scala
string1.concat(string2);
```

Aceasta returnează un string nou care este string1 cu string2 adăugat la el la sfârșit. De asemenea, puteți utiliza metoda concat() ca în −

```scala
"My name is ".concat("Zara");
```

String-urile de caractere sunt mai frecvent concatenate cu operatorul `+`, ca în −

```scala
"Hello," + " world" + "!"

result:
Hello, World!
```

```scala
object Demo {
   def main(args: Array[String]) {
      var str1 = "Dot saw I was ";
      var str2 =  "Tod";
      
      println("Dot " + str1 + str2);
   }
}

output:
Dot Dot saw I was Tod
```

## Formatarea String-urilor

Aveți metode `printf()` și `format()` pentru a imprima rezultate cu numere formatate. Clasa String are o metodă de clasă echivalentă, `format()`, care returnează un obiect String mai degrabă decât un obiect `PrintStream`.

Încercați următorul exemplu de program, care folosește metoda `printf()` -

```scala
object Demo {
   def main(args: Array[String]) {
      var floatVar = 12.456
      var intVar = 2000
      var stringVar = "Hello, Scala!"
      
      var fs = printf("The value of the float variable is " + "%f, while the value of the integer " + "variable is %d, and the string" + "is %s", floatVar, intVar, stringVar);
      
      println(fs)
   }
}

output:
The value of the float variable is 12.456000, 
while the value of the integer variable is 2000, 
and the string is Hello, Scala!()
```

## String interpolation

`String Interpolation` este noua modalitate de a crea șiruri în limbajul de programare Scala. Această caracteristică acceptă versiunile Scala-2.10 și ulterioare. Interpolarea string-urilor: mecanismul de a încorpora referințe variabile direct în literalul string-ului de proces.

Există trei tipuri (interpolatoare) de implementări în String Interpolation.

### The 's' String interpolator

Literalul „`s`” permite utilizarea variabilei direct în procesarea unui string, atunci când îi adăugați „`s`”. Orice variabilă String cu într-un domeniu care poate fi folosită într-un String. Următoarele sunt diferitele utilizări ale interpolatorului String „`s`”.

Următorul exemplu de fragment de cod pentru implementarea interpolatorului „`s`” în adăugarea variabilei String ($name) la un String normal (Bună ziua) în instrucțiunea println.

```scala
val name = “James”
println(s “Hello, $name”) //output: Hello, James
```

Interpolatorul de string-uri poate procesa și expresii arbitrare. Următorul fragment de cod pentru Procesarea unui string (1 + 1) cu expresie arbitrară (${1 + 1}) folosind interpolatorul String „`s`”. Orice expresie arbitrară poate fi încorporată în „`${}`”.

```scala
println(s “1 + 1 = ${1 + 1}”) //output: 1 + 1 = 2
```

```scala
object Demo {
   def main(args: Array[String]) {
      val name = "James"
      
      println(s"Hello, $name")
      println(s"1 + 1 = ${1 + 1}")
   }
}

output:
Hello, James
1 + 1 = 2
```

## The ‘ f ’ Interpolator

Interpolatorul literal „`f`” permite crearea unui string formatat, similar cu `printf` în limbajul C. Când utilizați interpolatorul „`f`”, toate referințele variabilelor ar trebui să fie urmate de specificatorii de format de stil printf, cum ar fi `%d`, `%i`, `%f` etc.

Să luăm un exemplu de adăugare a valorii în virgulă mobilă (`height = 1,9d`) și a variabilei String (`name = „James”`) cu string normal. Următorul fragment de cod al implementării interpolatorului `„f”`. Aici `$name%s` pentru a imprima (variabilă String) James și `$height%2.2f` pentru a imprima (valoare în virgulă mobilă) 1,90.

```scala
val height = 1.9d
val name = "James"
println(f"$name%s is $height%2.2f meters tall") //James is 1.90 meters tall
```

Este de tip sigur (adică, referința variabilei și următorul specificator de format ar trebui să se potrivească, altfel afișează eroare. Interpolatorul „`f`” folosește utilitarele de format String (specificatori de format) disponibile în Java. În mod implicit, nu există niciun caracter `%` după referința variabilei. Se va presupune ca `%s` (string)

## ‘raw’ Interpolator

Interpolatorul `raw` este similar cu interpolatorul `„s”`, cu excepția faptului că nu efectuează evadarea literalelor dintr-un string. Următoarele fragmente de cod dintr-un tabel vor diferi de utilizarea interpolatoarelor „`s`” și „`raw`”. În ieșirile utilizării „`s`”, „`\n`” are efect ca linie nouă și în ieșirea utilizării „`raw`” „`\n`” nu va avea efect. Acesta va imprima șirul complet cu litere de escape.


Exemplu `s` interpolator

```scala
object Demo {
   def main(args: Array[String]) {
      println(s"Result = \n a \n b")
   }
}

output:
Result =
a
b
```

Exemplu `raw` interpolator

```scala
object Demo {
   def main(args: Array[String]) {
      println(raw"Result = \n a \n b")
   }
}

output:
Result = \n a \n b
```

## Metodele String

Desigur, iată informațiile într-un format de tabel Markdown:

| Sr. No | Metodă                                       | Descriere                                                                                                          |
|-------|----------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| 1     | `charAt(int index)`                          | Returnează caracterul de la indexul specificat.                                                                     |
| 2     | `compareTo(Object o)`                        | Compară acest șir cu un alt obiect.                                                                                |
| 3     | `compareTo(String anotherString)`            | Compară două șiruri lexicografic.                                                                                 |
| 4     | `compareToIgnoreCase(String str)`            | Compară două șiruri lexicografic, ignorând diferențele de caz.                                                     |
| 5     | `concat(String str)`                         | Concatenează șirul specificat la sfârșitul acestui șir.                                                            |
| 6     | `contentEquals(StringBuffer sb)`             | Returnează adevărat dacă și numai dacă acest șir reprezintă aceeași secvență de caractere ca și StringBuffer specificat. |
| 7     | `copyValueOf(char[] data)`                   | Returnează un șir care reprezintă secvența de caractere din array-ul specificat.                                   |
| 8     | `copyValueOf(char[] data, int offset, int count)` | Returnează un șir care reprezintă secvența de caractere din array-ul specificat, începând de la un anumit offset și cu o anumită lungime. |
| 9     | `endsWith(String suffix)`                    | Verifică dacă acest șir se termină cu sufixul specificat.                                                           |
| 10    | `equals(Object anObject)`                    | Compară acest șir cu obiectul specificat.                                                                         |
| 11    | `equalsIgnoreCase(String anotherString)`    | Compară acest șir cu un alt șir, ignorând diferențele de caz.                                                     |
| 12    | `getBytes()`                                 | Encodează acest șir într-o secvență de octeți folosind setul de caractere implicit al platformei, stocând rezultatul într-un nou array de octeți. |
| 13    | `getBytes(String charsetName)`               | Encodează acest șir într-o secvență de octeți folosind setul de caractere specificat, stocând rezultatul într-un nou array de octeți. |
| 14    | `getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)` | Copiază caractere din acest șir în array-ul de caractere destinatar. |
| 15    | `hashCode()`                                | Returnează un cod hash pentru acest șir.                                                                         |
| 16    | `indexOf(int ch)`                            | Returnează indexul în acest șir al primei apariții a caracterului specificat.                                       |
| 17    | `indexOf(int ch, int fromIndex)`            | Returnează indexul în acest șir al primei apariții a caracterului specificat, pornind de la un anumit index.       |
| 18    | `indexOf(String str)`                       | Returnează indexul în acest șir al primei apariții a subșirului specificat.                                         |
| 19    | `indexOf(String str, int fromIndex)`        | Returnează indexul în acest șir al primei apariții a subșirului specificat, pornind de la un anumit index.          |
| 20    | `intern()`                                  | Returnează o reprezentare canonică pentru obiectul șir.                                                            |
| 21    | `lastIndexOf(int ch)`                       | Returnează indexul în acest șir al ultimei apariții a caracterului specificat.                                      |
| 22    | `lastIndexOf(int ch, int fromIndex)`       | Returnează indexul în acest șir al ultimei apariții a caracterului specificat, căutând înapoi începând de la un anumit index. |
| 23    | `lastIndexOf(String str)`                   | Returnează indexul în acest șir al ultimei apariții a subșirului specificat.                                         |
| 24    | `lastIndexOf(String str, int fromIndex)`    | Returnează indexul în acest șir al ultimei apariții a subșirului specificat, căutând înapoi începând de la un anumit index. |
| 25    | `length()`                                  | Returnează lungimea acestui șir.                                                                                  |
| 26    | `matches(String regex)`                     | Indică dacă acest șir se potrivește cu expresia regulată specificată.                                              |
| 27    | `regionMatches(boolean ignoreCase, int toffset, String other, int offset, int len)` | Testează dacă două regiuni ale șirurilor sunt egale, cu opțiunea de a ignora cazul. |
| 28    | `regionMatches(int toffset, String other, int offset, int len)` | Testează dacă două regiuni ale șirurilor sunt egale.                                                             |
| 29    | `replace(char oldChar, char newChar)`       | Returnează un nou șir rezultat din înlocuirea tuturor aparițiilor lui oldChar în acest șir cu newChar.              |
| 30    | `replaceAll(String regex, String replacement)` | Înlocuiește fiecare subșir al acestui șir care se potrivește cu expresia regulată dată cu înlocuirea dată. |
| 31    | `replaceFirst(String regex, String replacement)` | Înlocuiește primul subșir al acestui șir care se potrivește cu expresia regulată dată cu înlocuirea dată. |
| 32    | `split(String regex)`                       | Împarte acest șir în jurul potrivirilor expresiei regulate date.                                                   |
| 33    | `split(String regex, int limit)`            | Împarte acest șir în jurul potrivirilor expresiei regulate date, cu un număr limitat de elemente rezultate.         |
| 34    | `startsWith(String prefix)`                  | Verifică dacă acest șir începe cu prefixul specificat.                                                            |
| 35    | `startsWith(String prefix, int toffset)`    | Verifică dacă acest șir începe cu prefixul specificat, începând de la un anumit index.                             |
| 36    | `subSequence(int beginIndex, int endIndex)` | Returnează o nouă secvență de caractere care este o subsecvență a acestei secvențe.                                 |
| 37    | `substring(int beginIndex)`                  | Returnează un nou șir care este o subșir al acestui șir, începând de la un anumit index.                           |
| 38    | `substring(int beginIndex, int endIndex)`   | Returnează un nou șir care este o subșir al acestui șir, inclusiv caracterele de la un anumit index până la alt index. |
| 39    | `toCharArray()`                             | Convertește acest șir într-un nou array de caractere.                                                              |
| 40    | `toLowerCase()`                             | Convertește toate caracterele din acest șir la litere mici, folosind regulile locale implicite.                   |
| 41    | `toLowerCase(Locale locale)`                 | Convertește toate caracterele din acest șir la litere mici, folosind regulile locale date.                         |
| 42    | `toString()`                                | Returnează însuși obiectul (care este deja un șir!).                                                               |
| 43    | `toUpperCase()`                             | Convertește toate caracterele din acest șir la litere mari, folosind regulile locale implicite.                  |
| 44    | `toUpperCase(Locale locale)`                 | Convertește toate caracterele din acest șir la litere mari, folosind regulile locale date.                        |
| 45    | `trim()`                                    | Returnează o copie a șirului, eliminând spațiile albe de la început și sfârșit.                                     |
| 46    | `valueOf(primitive data type x)`             | Returnează reprezentarea șir a argumentului de tip primitiv.                                                       |
                                              |
```

Sper că aceasta este utilă!