# ParDo one-to-one


`ParDo` este o transformare în Apache Beam utilizată pentru procesarea paralelă generică. Paradigma de procesare a lui `ParDo` este similară cu faza "`Map`" a unui algoritm de tip `Map`/`Shuffle`/`Reduce`: o transformare `ParDo` consideră fiecare element din PCollection-ul de `input`, aplică o funcție de procesare (codul tău de utilizator) asupra acelui element și emite zero, unu sau mai mulți termeni către un PCollection de `Output`.

`ParDo` este util pentru o varietate de operațiuni comune de procesare a datelor, inclusiv:

- Filtrarea unui set de date. Puteți utiliza ParDo pentru a lua în considerare fiecare element dintr-un PCollection și fie să emiteți acel element către o nouă colecție, fie să îl eliminați.

- Formatarea sau conversia tipului fiecărui element dintr-un set de date. Dacă PCollection-ul dvs. de intrare conține elemente de un alt tip sau format decât doriți, puteți utiliza `ParDo` pentru a efectua o conversie asupra fiecărui element și să emiteți rezultatul către un nou PCollection.

- Extragerea părților din fiecare element dintr-un set de date. Dacă aveți un PCollection de înregistrări cu mai multe câmpuri, de exemplu, puteți utiliza un `ParDo` pentru a extrage doar câmpurile pe care doriți să le luați în considerare într-un nou PCollection.

- Efectuarea de calcule asupra fiecărui element dintr-un set de date. Puteți utiliza `ParDo` pentru a efectua calcule simple sau complexe asupra fiecărui element sau anumitor elemente dintr-un PCollection și să emiteți rezultatele către un nou PCollection.

În astfel de roluri, `ParDo` este o etapă intermediară comună într-un canal de procesare. Puteți să îl utilizați pentru a extrage anumite câmpuri dintr-un set de input-uri brute sau pentru a converti input-ul brut într-un format diferit; de asemenea, puteți utiliza `ParDo` pentru a converti datele procesate într-un format potrivit pentru output, cum ar fi rânduri de tabele de baze de date sau șiruri imprimabile.

Când aplicați o transformare `ParDo`, va trebui să furnizați codul de utilizator sub forma unui obiect `DoFn`. `DoFn` este o clasă din SDK-ul Apache Beam care definește o funcție de procesare distribuită.

## Aplicarea ParDo

`beam.ParDo` aplică argumentul transmis în `DoFn` la intrarea `PCcollection`, așa cum se arată în următorul exemplu de cod:

```java
// The input PCollection of Strings.
PCollection<String> input = ...;

// The DoFn to perform on each element in the input PCollection.
static class ComputeWordLengthFn extends DoFn<String, Integer> { ... }

// Apply a ParDo to the PCollection "input" to compute lengths for each word.
PCollection<Integer> wordLengths = input.apply(
ParDo
.of(new ComputeWordLengthFn())); // The DoFn to perform on each element, which
// we define above.
```

## **Crearea unui DoFn**

Obiectul `DoFn` pe care îl furnizezi lui `ParDo` conține logica de procesare care se aplică elementelor din colecția de input. Atunci când folosești Apache Beam, de multe ori cele mai importante părți ale codului pe care le vei scrie sunt aceste `DoFn`-uri - acestea definesc exact task-urile de prelucrare a datelor din pipeline-ul tău. 

**Notă**: Atunci când creezi `DoFn`-ul, fii atent la Cerințele pentru scrierea codului de utilizator pentru transformările Beam și asigură-te că codul tău le respectă.

Un `DoFn` procesează un element la un moment dat din PCollection-ul de input. Când creezi o subclasă a lui `DoFn`, va trebui să furnizezi parametri de tip care să se potrivească cu tipurile elementelor de input și de output.

Dacă `DoFn` procesează elemente `String` primite și produce elemente `Integer` pentru output (cum ar fi exemplul nostru anterior, `ComputeWordLengthFn`), declarația clasei dvs. ar arăta astfel:

```java
static class ComputeWordLengthFn extends DoFn<String, Integer> { ... }
```

În cadrul subclasei `DoFn`, vei scrie o metodă marcată cu `@ProcessElement`, în care furnizezi logica de procesare efectivă. Nu trebuie să extragi manual elementele din input; SDK-urile Beam se ocupă de acest lucru pentru tine. 

Metoda ta `@ProcessElement` ar trebui să accepte un parametru etichetat cu `@Element`, care va fi populat cu elementul de input. Pentru a emite elemente, metoda poate lua, de asemenea, un parametru de tip `OutputReceiver`, care oferă o metodă pentru emiterea elementelor. 

Tipurile de parametri trebuie să se potrivească cu tipurile de `input` și `output` ale `DoFn`-ului tău, altfel framework-ul va genera o eroare. 

**Notă**: `@Element` și `OutputReceiver` au fost introduse în Beam 2.5.0; dacă folosești o versiune mai veche a lui Beam, ar trebui să folosești în schimb un parametru `ProcessContext`.

```java
static class ComputeWordLengthFn extends DoFn<String, Integer> {
    @ProcessElement
    public void processElement(@Element String word, OutputReceiver<Integer> out) {
    // Use OutputReceiver.output to emit the output element.
    out.output(word.length());
    }
}
```

**Notă:** Indiferent dacă folosești un tip structural de DoFn sau un DoFn funcțional, acestea ar trebui să fie înregistrate cu Beam într-un bloc de inițializare (init block). În caz contrar, ele s-ar putea să nu fie executate pe runner-ii distribuiți.

**Notă:** Dacă elementele din PCollection-ul tău input sunt perechi cheie/valoare, metoda ta de procesare a elementelor trebuie să aibă doi parametri, unul pentru cheie și celălalt pentru valoare, respectiv. Similar, perechile cheie/valoare sunt, de asemenea, emise ca parametri separați către o singură funcție emițătoare.

O instanță dată a `DoFn` este, în general, invocată de una sau mai multe ori pentru a procesa un set arbitrar de elemente. Cu toate acestea, Beam nu garantează un număr exact de invocări; poate fi invocată de mai multe ori pe un nod de lucru dat pentru a ține cont de `failures` și `retries`. Astfel, poți să depozita informații pe parcursul mai multor apeluri la metoda ta de procesare, dar dacă o faci, asigură-te că implementarea nu depinde de numărul de invocări.

În metoda ta de procesare, va trebui să îndeplinești anumite cerințe de imutabilitate pentru a te asigura că Beam și motorul de procesare pot serializa și salva în siguranță valorile în pipeline-ul tău. Metoda ta ar trebui să îndeplinească următoarele cerințe:

- Nu ar trebui să modifici în niciun fel parametrii furnizați metodei `ProcessElement`, sau orice intrări secundare.
- Odată ce emiți o valoare folosind o funcție emițătoare, nu ar trebui să modifici acea valoare în niciun fel.

### Accesarea de parametri suplimentari în DoFn

În plus față de `@Element` și `OutputReceiver`, Beam va popula alți parametri pentru metoda `@ProcessElement` a DoFn-ului tău. Orice combinație a acestor parametri poate fi adăugată în metoda ta de procesare în orice ordine.

Timestamp: pentru a accesa marcajul de timp al unui element input, adăugați un parametru adnotat cu `@Timestamp` de tipul Instant. De exemplu:

```java
.of(new DoFn<String, String>() {
     public void processElement(@Element String word, @Timestamp Instant timestamp) {
  }})
```

### Window

Pentru a accesa window-ul în care un element input cade, adaugă un parametru de tipul window-ului utilizat pentru PCollection-ul input.

 Dacă parametrul este un tip de `window` (o subclasă a lui `BoundedWindow`) care nu se potrivește cu PCollection-ul input, atunci va fi generată o eroare. 
 
 Dacă un element cade în mai multe window-uri (de exemplu, atunci când se folosesc `Sliding Windows`), atunci metoda `@ProcessElement` va fi invocată de mai multe ori pentru element, o dată pentru fiecare window. De exemplu, atunci când se folosesc `Fixed Window`, window-ul este de tip `IntervalWindow`.

 ```java
 .of(new DoFn<String, String>() {
public void processElement(@Element String word, IntervalWindow window) {
}})
 ```

### PaneInfo:

 Atunci când se folosesc triggere în Beam, acesta furnizează un obiect `PaneInfo` care conține informații despre current firing. Utilizând `PaneInfo`, poți determina dacă aceasta este o declanșare `early` sau `late`, și de câte ori window-ul curent a fost deja fired pentru această cheie.

 ```java
 .of(new DoFn<String, String>() {
     public void processElement(@Element String word, PaneInfo paneInfo) {
  }})
 ```

 ### PipelineOptions: 
 
 `PipelineOptions` pentru pipeline-ul curent poate fi întotdeauna accesat într-o metodă de procesare prin adăugarea acestuia ca parametru:

 ```java
 .of(new DoFn<String, String>() {
     public void processElement(@Element String word, PipelineOptions options) {
  }})
 ```

 Metodele `@OnTimer` pot, de asemenea, să acceseze multe dintre acești parametri. Parametrii cum ar fi `Timestamp`, `Window`, `key`, `PipelineOptions`, `OutputReceiver` și `MultiOutputReceiver` pot fi accesați într-o metodă `@OnTimer`. În plus, o metodă `@OnTimer` poate lua un parametru de tip `TimeDomain` care indică dacă cronometrul se bazează pe timpul evenimentului sau pe timpul de procesare. Timerele sunt explicate în detaliu în postarea de blog `Timely` (and `Stateful`) Processing with Apache Beam.

 Exemplu complet:

 ```java
 import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.transforms.*;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);


    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        // List of elements
        PCollection<Integer> input =
                pipeline.apply(Create.of(1, 2, 3, 4, 5));

        // The applyTransform() converts [input] to [output]
        PCollection<Integer> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<Integer>()));

        pipeline.run();
    }

    // The applyTransform() multiplies the number by 10 and outputs
    static PCollection<Integer> applyTransform(PCollection<Integer> input) {
        return input.apply(ParDo.of(new DoFn<Integer, Integer>() {

            @ProcessElement
            public void processElement(@Element Integer number, OutputReceiver<Integer> out) {
                out.output(number * 10);
            }

        }));
    }

    static class LogOutput<T> extends DoFn<T, T> {
        private String prefix;

        LogOutput() {
            this.prefix = "Processing element";
        }
        
        LogOutput(String prefix) {
            this.prefix = prefix;
        }

        @ProcessElement
        public void processElement(ProcessContext c) throws Exception {
            LOG.info(prefix + ": {}", c.element());
        }
    }
}
 ```