# Metodele String

| Metodă                | Descriere                                                                                                   | Tipul Rezultatului |
|-----------------------|------------------------------------------------------------------------------------------------------------|---------------------|
| charAt()              | Returnează caracterul de la indexul specificat (poziție).                                                    | char                |
| codePointAt()         | Returnează codul Unicode al caracterului de la indexul specificat.                                           | int                 |
| codePointBefore()     | Returnează codul Unicode al caracterului înaintea indexului specificat.                                       | int                 |
| codePointCount()      | Returnează numărul de valori Unicode găsite într-un șir de caractere.                                        | int                 |
| compareTo()           | Compară două șiruri lexicografic.                                                                          | int                 |
| compareToIgnoreCase() | Compară două șiruri lexicografic, ignorând diferențele de majuscule și minuscule.                           | int                 |
| concat()              | Atașează un șir la sfârșitul altui șir.                                                                    | String              |
| contains()            | Verifică dacă un șir conține o secvență de caractere.                                                       | boolean             |
| contentEquals()       | Verifică dacă un șir conține exact aceeași secvență de caractere ca și CharSequence sau StringBuffer specificat. | boolean             |
| copyValueOf()         | Returnează un șir care reprezintă caracterele unui tablou de caractere.                                      | String              |
| endsWith()            | Verifică dacă un șir se termină cu caracterele specificate.                                                  | boolean             |
| equals()              | Compară două șiruri. Returnează true dacă șirurile sunt egale și false în caz contrar.                      | boolean             |
| equalsIgnoreCase()    | Compară două șiruri, ignorând diferențele de majuscule și minuscule.                                        | boolean             |
| format()              | Returnează un șir format utilizând locale, șir de format și argumente specificate.                         | String              |
| getBytes()            | Codifică acest șir într-o secvență de octeți folosind charset-ul specificat și stochează rezultatul într-un nou tablou de octeți. | byte[]              |
| getChars()            | Copiază caracterele dintr-un șir într-un tablou de caractere.                                                | void                |
| hashCode()           | Returnează codul de dispersie al unui șir.                                                                  | int                 |
| indexOf()            | Returnează poziția primei apariții a caracterelor specificate într-un șir.                                  | int                 |
| intern()              | Returnează reprezentarea canonică a obiectului de șir.                                                       | String              |
| isEmpty()            | Verifică dacă un șir este gol sau nu.                                                                      | boolean             |
| lastIndexOf()         | Returnează poziția ultimei apariții a caracterelor specificate într-un șir.                                  | int                 |
| length()              | Returnează lungimea unui șir specificat.                                                                   | int                 |
| matches()            | Caută un șir pentru o potrivire cu o expresie regulată și returnează potrivirile.                           | boolean             |
| offsetByCodePoints()  | Returnează indexul din acest șir care este compensat de indexul dat de codePointOffset code points.         | int                 |
| regionMatches()       | Testează dacă două regiuni de șiruri sunt egale.                                                            | boolean             |
| replace()            | Caută un șir pentru o valoare specificată și returnează un nou șir în care valorile specificate sunt înlocuite. | String              |
| replaceFirst()       | Înlocuiește prima apariție a unei subșiruri care se potrivește cu expresia regulată dată, cu înlocuirea dată. | String              |
| replaceAll()         | Înlocuiește fiecare subșir al acestui șir care se potrivește cu expresia regulată dată, cu înlocuirea dată.  | String              |
| split()              | Desparte un șir într-un tablou de subșiruri.                                                               | String[]            |
| startsWith()         | Verifică dacă un șir începe cu caracterele specificate.                                                    | boolean             |
| subSequence()        | Returnează o nouă secvență de caractere care este o subsecvență a acestei secvențe.                        | CharSequence        |
| substring()          | Returnează un nou șir care este o subșir al unui șir specificat.                                            | String              |
| toCharArray()        | Convertește acest șir într-un nou tablou de caractere.                                                     | char[]              |
| toLowerCase()        | Convertește un șir în litere mici.                                                                         | String              |
| toString()           | Returnează valoarea unui obiect String.                                                                    | String              |
| toUpperCase()        | Convertește un șir în litere mari.                                                                        | String              |
| trim()               | Elimină spațiile albe de la ambele capete ale unui șir.                                                     | String              |
| valueOf()            | Returnează reprezentarea sub formă de șir a valorii specificate.                                           | String              |
