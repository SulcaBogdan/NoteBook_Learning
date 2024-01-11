# PCollections in Apache Beam

# Crearea unui PColection

Acum că știi cum să creezi un `pipeline` Beam și să transmiți parametri în el, este timpul să înveți cum să creezi o `PCollection` inițială și să o umpli cu date. Există mai multe opțiuni:

- Poți crea un PCollection de date stocate într-o clasă de colecție în memorie în programul tău.
- Poți, de asemenea, să citești datele din diverse surse externe precum fișiere locale sau bazate pe cloud, baze de date sau alte surse folosind adaptatoarele `I/O` furnizate de Beam.

Pe parcursul turului, majoritatea exemplelor folosesc fie o PCollection creată din date în memorie, fie date citite dintr-unul dintre containerele cloud "beam-examples" sau "dataflow-samples". Aceste containere conțin seturi de date de exemplu create special în scopuri educaționale.

Te încurajăm să arunci o privire, să explorezi aceste seturi de date și să le folosești în timp ce înveți despre Apache Beam.

## Crearea de in-memory PColection

Poți utiliza transformarea Create furnizată de Beam pentru a crea o PCollection dintr-o colecție în memorie. Poți aplica transformarea Create direct la obiectul tău Pipeline însuși.

Exemplul următor arată cum să faci acest lucru:


```java
public static void main(String[] args) {
    // First create the pipeline
    PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
    Pipeline pipeline = Pipeline.create(options);

    // Now create the PCollection using list of strings
    PCollection<String> strings =
    pipeline.apply(
    Create.of("To", "be", "or", "not", "to", "be","that", "is", "the", "question")
    );

    // Create a numerical PCollection
    PCollection<Integer> numbers =
    pipeline.apply(
    Create.of(1,2,3,4,5,6,7,8,9,10)
    );
}
```

Puteți găsi codul complet al acestui exemplu mai jos.

Una dintre diferențe pe care le veți observa este că conține și partea pentru a afișa elementele PCollection în consolă. Nu vă faceți griji dacă încă nu înțelegeți complet, deoarece conceptul de transformare `ParDo` va fi explicat mai târziu în curs.

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.Create;
import org.apache.beam.sdk.transforms.Min;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.transforms.DoFn;
import org.apache.beam.sdk.transforms.ParDo;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {

        LOG.info("Running Task");

        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        PCollection<String> words =
                pipeline.apply(
                        Create.of("To", "be", "or", "not", "to", "be","that", "is", "the", "question")
                );

        PCollection<Integer> numbers =
                pipeline.apply(
                        Create.of(1,2,3,4,5,6,7,8,9,10)
                );

        words.apply("Log words", ParDo.of(new LogStrings()));
        numbers.apply("Log numbers", ParDo.of(new LogIntegers()));


        pipeline.run();
    }


    public static class LogStrings extends DoFn<String, String> {

        @ProcessElement
        public void processElement(ProcessContext c) throws Exception {
            LOG.info("Processing word: {}", c.element());
            c.output(c.element());
        }
    }

    public static class LogIntegers extends DoFn<Integer, Integer> {

        @ProcessElement
        public void processElement(ProcessContext c) throws Exception {
            LOG.info("Processing number: {}", c.element());
            c.output(c.element());
        }
    }
}
```

## Crearea unui PCollection dintr-un text file

### Citirea dintr-un fișier text

Folosești unul dintre adaptatoarele I/O furnizate de Beam pentru a citi dintr-o sursă externă. Adaptoarele variază în utilizarea exactă, dar toate citesc dintr-o sursă de date externă și returnează un PCollection a cărui elemente reprezintă înregistrările de date din acea sursă.

Fiecare adaptor de sursă de date are o transformare `Read`; pentru a citi, trebuie să aplici acea transformare direct obiectului tău `Pipeline` însuși. `TextIO.Read`, de exemplu, citește dintr-un fișier text extern și returnează un PCollection a cărui elemente sunt de tip String. Fiecare String reprezintă o linie din fișierul text. Iată cum ai aplica `TextIO.Read` la Pipeline-ul tău pentru a crea o PCollection:

```java
public static void main(String[] args) {
    // First create the pipeline
    PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
    Pipeline pipeline = Pipeline.create(options);

    // Now create the PCollection by reading text files. Separate elements will be added for each line in the input file
    PCollection<String> input =
    pipeline.apply(“King Lear”,TextIO.read().from("gs://apache-beam-samples/shakespeare/kinglear.txt")
    );

}
```
Mai jos, poți găsi un exemplu care citește un poem "King Lear" dintr-un fișier text stocat în depozitul `Google Storage` și umple `PCollection` cu linii individuale, apoi cu cuvinte individuale.

Una dintre diferențele pe care le veți observa este că ieșirea este mult mai scurtă decât fișierul de intrare în sine. Acest lucru se datorează faptului că numărul de elemente din PCollection-ul de ieșire este limitat cu transformarea `Sample.fixedSizeGlobally`. Utilizarea `Sample.fixedSizeGlobally` este o altă tehnică pe care o puteți utiliza pentru a depana și limita ieșirea trimisă la consolă în scopuri de depanare în cazul seturilor de date de intrare mari.

```java
package org.apache.beam.examples;

import java.util.Arrays;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.io.TextIO;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.Count;
import org.apache.beam.sdk.transforms.DoFn;
import org.apache.beam.sdk.transforms.Filter;
import org.apache.beam.sdk.transforms.Flatten;
import org.apache.beam.sdk.transforms.FlatMapElements;
import org.apache.beam.sdk.transforms.MapElements;
import org.apache.beam.sdk.transforms.ParDo;
import org.apache.beam.sdk.transforms.PTransform;
import org.apache.beam.sdk.transforms.Sample;
import org.apache.beam.sdk.values.KV;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.values.TypeDescriptors;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);


    public static void main(String[] args) {

        PipelineOptions options = PipelineOptionsFactory.create();

        // Create the Pipeline object with the options we defined above
        Pipeline pipeline = Pipeline.create(options);

        // Concept #1. Read text file content line by line. resulting PCollection contains elements, where each element
        // contains a single line of text from the input file.
        PCollection<String> input = pipeline.apply(TextIO.read().from("gs://apache-beam-samples/shakespeare/kinglear.txt"))
                .apply(Filter.by((String line) -> !line.isEmpty()));

        // Concept #2. Output first 10 elements PCollection to the console.
        final PTransform<PCollection<String>, PCollection<Iterable<String>>> sample = Sample.fixedSizeGlobally(10);

        PCollection<String> sampleLines = input.apply(sample)
                .apply(Flatten.iterables())
                .apply("Log lines", ParDo.of(new LogStrings()));

        //Concept #3. Read text file and split into PCollection of words.
        PCollection<String> words = pipeline.apply(TextIO.read().from("gs://apache-beam-samples/shakespeare/kinglear.txt"))
                .apply(FlatMapElements.into(TypeDescriptors.strings()).via((String line) -> Arrays.asList(line.split("[^\\p{L}]+"))))
                .apply(Filter.by((String word) -> !word.isEmpty()));

        PCollection<String> sampleWords = words.apply(sample)
                .apply(Flatten.iterables())
                .apply("Log words", ParDo.of(new LogStrings()));

        // Concept #4. Write PCollection to text file.
        sampleWords.apply(TextIO.write().to("sample-words"));
        pipeline.run().waitUntilFinish();
    }

    public static class LogStrings extends DoFn<String, String> {

        @ProcessElement
        public void processElement(ProcessContext c) throws Exception {
            LOG.info("Processing element: {}", c.element());
            c.output(c.element());
        }
    }
}
```

## Crearea unui PCollection dintr-un csv file

### Citirea dintr-un fișier CSV

Fluxurile de prelucrare a datelor lucrează adesea cu date tabulare. În multe exemple și provocări pe parcursul cursului, veți lucra cu unul dintre seturile de date stocate sub formă de fișiere CSV în containerele beam-examples, `dataflow-samples`.Încărcarea datelor dintr-un fișier CSV necesită unele procesări și constă în două părți principale:

• Încărcarea liniilor de text folosind transformarea `TextIO.Read`
• Parsarea liniilor de text în format tabular

| cost | passenger_count | ... |
|------|------------------|-----|
| 5.81 | 4.62             | ... |
| 4.6  | 2                | ... |
| 24   | 1                | ... |

```java
import java.util.Arrays;
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.io.TextIO;

import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.Count;
import org.apache.beam.sdk.transforms.Filter;
import org.apache.beam.sdk.transforms.FlatMapElements;
import org.apache.beam.sdk.transforms.MapElements;
import org.apache.beam.sdk.transforms.PTransform;
import org.apache.beam.sdk.values.KV;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.values.TypeDescriptors;
import org.apache.beam.sdk.transforms.Flatten;
import org.apache.beam.sdk.transforms.Sample;
import org.apache.beam.sdk.transforms.DoFn;
import org.apache.beam.sdk.transforms.ParDo;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;


public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);


    public static void main(String[] args) {

        PipelineOptions options = PipelineOptionsFactory.create();

        // Create the Pipeline object with the options we defined above
        Pipeline pipeline = Pipeline.create(options);
        PCollection<String> input = pipeline.apply(TextIO.read().from("gs://apache-beam-samples/nyc_taxi/misc/sample1000.csv"));

        PCollection<Double> rideTolalAmounts = input.apply(ParDo.of(new ExtractTaxiRideCostFn()));
        final PTransform<PCollection<Double>, PCollection<Iterable<Double>>> sample = Sample.fixedSizeGlobally(10);
        PCollection<Double> rideAmounts = rideTolalAmounts.apply(sample)
                .apply(Flatten.iterables())
                .apply("Log amounts", ParDo.of(new LogDouble()));

        pipeline.run().waitUntilFinish();

    }

    private static Double tryParseTaxiRideCost(String[] inputItems) {
        try {
            return Double.parseDouble(tryParseString(inputItems, 16));
        } catch (NumberFormatException | NullPointerException e) {
            return 0.0;
        }
    }


    private static String tryParseString(String[] inputItems, int index) {
        return inputItems.length > index ? inputItems[index] : null;
    }

    static class ExtractTaxiRideCostFn extends DoFn<String, Double> {

        @ProcessElement
        public void processElement(ProcessContext c) {
            String[] items = c.element().split(",");
            Double totalAmount = tryParseTaxiRideCost(items);
            c.output(totalAmount);
        }
    }

    public static class LogDouble extends DoFn<Double, Double> {

        @ProcessElement
        public void processElement(ProcessContext c) throws Exception {
            LOG.info("Total Amount: {}", c.element());
            c.output(c.element());
        }
    }
}
```