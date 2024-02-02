# CoGroupByKey in Apache Beam

Puteți utiliza transformarea `CoGroupByKey` pentru o tuplă de tabele. `CoGroupByKey` grupează rezultatele din toate tabelele după chei similare în `CoGbkResults`, din care rezultatele pentru oricare tabel particular pot fi accesate folosind `TupleTag` furnizat cu tabelul sursă.

Pentru siguranța tipului, SDK-ul Java vă cere să treceți fiecare PCollection ca parte a unui `KeyedPCollectionTuple`. Trebuie să declarați un `TupleTag` pentru fiecare `PCollection` de intrare în `KeyedPCollectionTuple` pe care doriți să o treceți la `CoGroupByKey`. Ca rezultat, `CoGroupByKey` returnează un `PCollection<KV<K, CoGbkResult>>`, care grupează valorile din toate PCollections input după cheile comune. Fiecare cheie (toate de tipul K) va avea un `CoGbkResult` diferit, care este o hartă de la `TupleTag<T>` la `Iterable<T>`. Puteți accesa o colecție specifică într-un obiect `CoGbkResult` folosind TupleTag pe care l-ați furnizat cu colecția inițială.

```java
// Mock data
final List<KV<String, String>> emailsList =
    Arrays.asList(
        KV.of("amy", "amy@example.com"),
        KV.of("carl", "carl@example.com"),
        KV.of("julia", "julia@example.com"),
        KV.of("carl", "carl@email.com"));

final List<KV<String, String>> phonesList =
    Arrays.asList(
        KV.of("amy", "111-222-3333"),
        KV.of("james", "222-333-4444"),
        KV.of("amy", "333-444-5555"),
        KV.of("carl", "444-555-6666"));

// Creating PCollections
PCollection<KV<String, String>> emails = p.apply("CreateEmails", Create.of(emailsList));
PCollection<KV<String, String>> phones = p.apply("CreatePhones", Create.of(phonesList));

// Create TupleTag for safety type
final TupleTag<String> emailsTag = new TupleTag<>();
final TupleTag<String> phonesTag = new TupleTag<>();

// Apply CoGroupByKey
PCollection<KV<String, CoGbkResult>> results =
    KeyedPCollectionTuple.of(emailsTag, emails)
        .and(phonesTag, phones)
        .apply(CoGroupByKey.create());

// Get result
PCollection<String> contactLines =
    results.apply(
        ParDo.of(
            new DoFn<KV<String, CoGbkResult>, String>() {
              @ProcessElement
              public void processElement(ProcessContext c) {
                KV<String, CoGbkResult> e = c.element();
                String name = e.getKey();
                Iterable<String> emailsIter = e.getValue().getAll(emailsTag);
                Iterable<String> phonesIter = e.getValue().getAll(phonesTag);
                String formattedResult =
                    Snippets.formatCoGbkResults(name, emailsIter, phonesIter);
                c.output(formattedResult);
              }
            }));
```


Următorul exemplu de cod realizează o uniune a două `PCollections` cu `CoGroupByKey`, urmată de un `ParDo` pentru a consuma rezultatul. Apoi, codul folosește etichete pentru a căuta și formata datele din fiecare colecție.


În cod, am combinat datele folosind primele litere ale fructelor și primele litere ale țărilor. Și rezultatul a fost astfel: (Alfabet) cheie: prima literă, (Țară) valori-1:Țară, (Fruct) valori-2:Fructe. Puteți lucra cu date de tip cheie-valoare pregătite, de exemplu, dacă doriți să le combinați folosind țările și să afișați greutatea fructului:

```java
PCollection<KV<String,Integer>> weightPCollection = pipeline.apply("Countries",
                        Create.of(KV.of("australia", 1000),
                                  KV.of("brazil", 150),
                                  KV.of("canada", 340))
);

PCollection<KV<String,String>> fruitsPCollection = pipeline.apply("Friuts",
                        Create.of(KV.of("australia", "cherry"),
                                  KV.of("brazil", "apple"),
                                  KV.of("canada", "banan"))
);
```

Schimbam `WordsAlphabet` to `ProductWeight`:

```java
static class ProductWeight {
        private String country;
        private String fruit;
        private Integer productWeight;

        public WordsAlphabet(String country, String fruit, Integer productWeight) {
            this.country = country;
            this.fruit = fruit;
            this.productWeight = productWeight;
        }

        // ToString...
}
```

Unirea are loc prin tastele:

```java
static PCollection<String> applyTransform(PCollection<String> fruits, PCollection<String> countries) {
        TupleTag<String> fruitsTag = new TupleTag<>();
        TupleTag<String> productWeightTag = new TupleTag<>();

        MapElements<String, KV<String, String>> mapToAlphabetKv =
                MapElements.into(kvs(strings(), strings()))
                        .via(word -> KV.of(word.substring(0, 1), word));

        PCollection<KV<String, String>> fruitsPColl = fruits.apply("Fruit to KV", mapToAlphabetKv);
        PCollection<KV<String, String>> countriesPColl = countries
                .apply("Country to KV", mapToAlphabetKv);

        return KeyedPCollectionTuple
                .of(fruitsTag, fruitsPCollection)
                .and(productWeightTag, weightPCollection)
                .apply(CoGroupByKey.create())
                .apply(ParDo.of(new DoFn<KV<String, CoGbkResult>, String>() {

                    @ProcessElement
                    public void processElement(
                            @Element KV<String, CoGbkResult> element, OutputReceiver<String> out) {

                        String alphabet = element.getKey();
                        CoGbkResult coGbkResult = element.getValue();

                        String fruit = coGbkResult.getOnly(fruitsTag);
                        String country = coGbkResult.getOnly(countriesTag);

                        out.output(new WordsAlphabet(alphabet, fruit, country).toString());
                    }

                }));
}
```


Exemplu complet:

```java
import static org.apache.beam.sdk.values.TypeDescriptors.kvs;
import static org.apache.beam.sdk.values.TypeDescriptors.strings;

import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.Create;
import org.apache.beam.sdk.transforms.DoFn;
import org.apache.beam.sdk.transforms.MapElements;
import org.apache.beam.sdk.transforms.ParDo;
import org.apache.beam.sdk.transforms.join.CoGbkResult;
import org.apache.beam.sdk.transforms.join.CoGroupByKey;
import org.apache.beam.sdk.transforms.join.KeyedPCollectionTuple;
import org.apache.beam.sdk.values.KV;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.values.TupleTag;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);
    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        PCollection<String> fruits =
                pipeline.apply("Fruits",
                        Create.of("apple", "banana", "cherry")
                );

        PCollection<String> countries =
                pipeline.apply("Countries",
                        Create.of("australia", "brazil", "canada")
                );

        PCollection<String> output = applyTransform(fruits, countries);

        output.apply(ParDo.of(new LogOutput<>()));

        pipeline.run();
    }

    static PCollection<String> applyTransform(
            PCollection<String> fruits, PCollection<String> countries) {

        TupleTag<String> fruitsTag = new TupleTag<>();
        TupleTag<String> countriesTag = new TupleTag<>();

        MapElements<String, KV<String, String>> mapToAlphabetKv =
                MapElements.into(kvs(strings(), strings()))
                        .via(word -> KV.of(word.substring(0, 1), word));

        PCollection<KV<String, String>> fruitsPColl = fruits.apply("Fruit to KV", mapToAlphabetKv);
        PCollection<KV<String, String>> countriesPColl = countries
                .apply("Country to KV", mapToAlphabetKv);

        return KeyedPCollectionTuple
                .of(fruitsTag, fruitsPColl)
                .and(countriesTag, countriesPColl)

                .apply(CoGroupByKey.create())

                .apply(ParDo.of(new DoFn<KV<String, CoGbkResult>, String>() {

                    @ProcessElement
                    public void processElement(
                            @Element KV<String, CoGbkResult> element, OutputReceiver<String> out) {

                        String alphabet = element.getKey();
                        CoGbkResult coGbkResult = element.getValue();

                        String fruit = coGbkResult.getOnly(fruitsTag);
                        String country = coGbkResult.getOnly(countriesTag);

                        out.output(new WordsAlphabet(alphabet, fruit, country).toString());
                    }

                }));
    }

     static class WordsAlphabet {

        private String alphabet;
        private String fruit;
        private String country;

        public WordsAlphabet(String alphabet, String fruit, String country) {
            this.alphabet = alphabet;
            this.fruit = fruit;
            this.country = country;
        }

        @Override
        public String toString() {
            return "WordsAlphabet{" +
                    "alphabet='" + alphabet + '\'' +
                    ", fruit='" + fruit + '\'' +
                    ", country='" + country + '\'' +
                    '}';
        }
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
