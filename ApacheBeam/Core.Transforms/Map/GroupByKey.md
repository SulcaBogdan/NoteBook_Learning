# GroupByKey in Apache Beam

`GroupByKey` este o transformare folosită pentru a grupa elementele într-un PCollection după cheie. Intrarea pentru `GroupByKey` este un PCollection de perechi **cheie-valoare**, în care cheile sunt utilizate pentru a grupa elementele. Output-ul pentru `GroupByKey` este un PCollection de perechi cheie-valoare, unde cheile sunt aceleași ca în input, iar valorile sunt liste de toate elementele cu acea cheie.

Să examinăm mecanica `GroupByKey` cu un exemplu simplu, în cazul în care setul nostru de date constă în cuvinte dintr-un fișier text și numărul liniei în care apar. Dorim să grupăm împreună toate numerele de linii (valori) care partajează același cuvânt (cheie), permițându-ne să vedem toate locurile din text în care apare un cuvânt specific.

Intrarea noastră este un PCollection de perechi cheie/valoare în care fiecare cuvânt este o cheie, iar valoarea este un număr de linie în fișierul în care apare cuvântul. Iată o listă de perechi cheie/valoare în colecția input:

```java
cat, 1
dog, 5
and, 1
jump, 3
tree, 2
cat, 5
dog, 2
and, 2
cat, 9
and, 6
```

`GroupByKey` adună toate valorile cu aceeași cheie și produce o nouă pereche formată din cheia unică și o colecție a tuturor valorilor asociate cu acea cheie în colecția de intrare. Dacă aplicăm `GroupByKey` pe colecția noastră de intrare de mai sus, colecția de ieșire ar arăta astfel:

```java
cat, [1,5,9]
dog, [5,2]
and, [1,2,6]
jump, [3]
tree, [2]
```

Prin urmare, `GroupByKey` reprezintă o transformare de la un `multimap` (multiple chei la valori individuale) la o `uni-map` (chei unice la colecții de valori).

```java
// The input PCollection.
PCollection<KV<String, String>> input = ...;

// Apply GroupByKey to the PCollection input.
// Save the result as the PCollection reduced.
PCollection<KV<String, Iterable<String>>> reduced = mapped.apply(GroupByKey.<String, String>create());
```

## GroupByKey și unbounded PCollections

Dacă utilizați unbounded `PCollections`, trebuie să utilizați fie un window non-global, fie un declanșator de agregare pentru a efectua o operație `GroupByKey` sau `CoGroupByKey`. Acest lucru se datorează faptului că un `GroupByKey` sau `CoGroupByKey` delimitat trebuie să aștepte ca toate datele cu o anumită cheie să fie colectate, dar cu colecții nelimitate, datele sunt nelimitate. Window-urile și/sau triggerele permit gruparea să opereze pe grupuri logice, finite de date în cadrul `unbounded data streams`.

Dacă aplicați `GroupByKey` sau `CoGroupByKey` la un grup de unbounded `PCollections`  fără a seta fie o strategie de  window-uri non-globale, fie o strategie de trigger sau ambele pentru fiecare colecție, Beam generează o eroare `IllegalStateException` la construcția timpului de execuție a pipeline-ului.

Când utilizați `GroupByKey` sau `CoGroupByKey` pentru a grupa `PCollections` care au o strategie de windowing aplicată, toate PCollections pe care doriți să le grupați trebuie să utilizeze aceeași strategie de windowing și window sizing. De exemplu, toate colecțiile pe care le uniți trebuie să utilizeze `fixed windows` identice de 5 minute (hipotetic) sau sliding windows de 4 minute care încep în fiecare 30 de secunde.

Dacă pipeline-ul dvs. încearcă să utilizeze `GroupByKey` sau `CoGroupByKey` pentru a uni PCollections cu window-uri incompatibile, Beam generează o eroare `IllegalStateException` la construcția timpului de execuție a pipeline-ului.

Exemplu complet:

```java
import static org.apache.beam.sdk.values.TypeDescriptors.kvs;
import static org.apache.beam.sdk.values.TypeDescriptors.strings;

import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.values.KV;
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
        PCollection<String> input =
                pipeline.apply(
                        Create.of("apple", "ball", "car", "bear", "cheetah", "ant")
                );
        // The applyTransform() converts [words] to [output]
        PCollection<KV<String, Iterable<String>>> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<KV<String, Iterable<String>>>()));

        pipeline.run();
    }   

     // The method returns a map which key will be the first letter, and the values are a list of words
    static PCollection<KV<String, Iterable<String>>> applyTransform(PCollection<String> input) {
        return input
                .apply(MapElements.into(kvs(strings(), strings()))
                        .via(word -> KV.of(word.substring(0, 1), word)))

                .apply(GroupByKey.create());
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
