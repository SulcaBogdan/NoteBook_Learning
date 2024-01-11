# Termenii Apache Beam

- **`Pipeline`:** Un flux de lucru este un graf construit de utilizator de transformări care definesc operațiile dorite de prelucrare a datelor.
- **`PCollection`:** O PCollection este un set de date sau un flux de date. Datele procesate de un flux de lucru fac parte dintr-o PCollection.
- **`PTransform`:** Un PTransform (sau transformare) reprezintă o operație de prelucrare a datelor sau un pas în fluxul tău de lucru. O transformare este aplicată la zero sau mai multe obiecte PCollection și produce zero sau mai multe obiecte PCollection.
- **`Aggregation `:** Aggregation este calcularea unei valori din mai multe elemente de input (1 sau mai multe).
- **`User-defined function (UDF)`:** Anumite operații Beam permit rularea de cod definit de utilizator ca o modalitate de a configura transformarea.
- **`Schema`:** Un schema este o definiție de tip independent de limbaj pentru o PCollection. Schematizarea unei PCollection definește elementele acelei PCollection ca o listă ordonată de câmpuri numite.
- **`SDK`:** O bibliotecă specifică unui limbaj care permite autorilor de fluxuri de lucru să construiască transformări, să-și construiască pipeline-urile și să le trimită la un runner.
- **`Runner`:** Un runner rulează un pipeline Beam folosind capacitățile motorului ales de prelucrare a datelor.
- **`Window`:** O PCollection poate fi subdivizată în ferestre bazate pe marcajele temporale ale elementelor individuale. Ferestrele permit operații de grupare asupra colecțiilor care cresc în timp prin divizarea colecției în ferestre de colecții finite.
- **`Watermark`:** Un Watermark este o estimare a momentului în care se așteaptă ca toate datele dintr-un anumit window să fi ajuns. Acest lucru este necesar pentru că nu întotdeauna datele sunt garantate să ajungă într-un pipeline în ordinea timpului evenimentului sau să ajungă întotdeauna la intervale previzibile.
- **`Trigger`:** Un trigger determină când să agregăm rezultatele fiecărei ferestre.
- **`State and timers`:** State and timers sunt primitive la un nivel mai scăzut, care îți oferă control total asupra agregării colecțiilor de input care cresc în timp.
- **`Splittable DoFn`:** Splittable DoFns îți permit să procesezi elemente într-un mod non-monolitic. Poți salva stadiul de procesare al unui element, iar runner-ul poate împărți restul lucrărilor pentru a obține paralelism suplimentar.

