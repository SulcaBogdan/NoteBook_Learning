# Transformarea Filter in Apache Beam

### Folosind Filter pentru PCollection

Seturile de date pot fi filtrate folosind transformarea `Filter`. Poți crea un filtru furnizând o predicție și, atunci când este aplicat, filtrează toate elementele din PCollection care nu satisfac predicția.

```java
PCollection<String> input = pipeline
.apply(Create.of(List.of("Hello","world","Hi")));

PCollection<String> filteredStrings = input
.apply(Filter.by(new SerializableFunction<String, Boolean>() {
@Override
public Boolean apply(String input) {
return input.length() > 3;
}
}));
```

Output:

```java
Hello
world
```

## Build-in filters

SDK-ul Java are mai multe metode build-in de filtrare, cum ar fi `Filter.greaterThan` și `Filter.lessThan`. Cu `Filter.greaterThan`, PCollection-ul de input poate fi filtrat astfel încât să rămână doar elementele ale căror valori sunt mai mari decât cantitatea specificată. Similar, poți utiliza `Filter.lessThan` pentru a filtra elementele din PCollection-ul de intrare ale căror valori sunt mai mari decât cantitatea specificată.

Alte metode build-in sunt:
- `Filter.greaterThanEq`
- `Filter.greaterThan`
- `Filter.lessThan`
- `Filter.lessThanEq`
- `Filter.equal`

### Exemplu de filtrare folosing metode build-in

```java
// List of integers
PCollection<Integer> input = pipeline.apply(Create.of(List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)));

PCollection<Integer> greaterThanEqNumbers = input.apply(Filter.greaterThanEq(3));
// PCollection will contain [3, 4, 5, 6, 7, 8, 9, 10] at this point

PCollection<Integer> greaterThanNumbers = input.apply(Filter.greaterThan(4));
// PCollection will contain [5, 6, 7, 8, 9, 10] at this point


PCollection<Integer> lessThanNumbers = input.apply(Filter.lessThan(10));
// PCollection will contain [1, 2, 3, 4, 5, 6, 7, 8, 9] at this point


PCollection<Integer> lessThanEqNumbers = input.apply(Filter.lessThanEq(7));
// PCollection will contain [1, 2, 3, 4 5, 6, 7] at this point


PCollection<Integer> equalNumbers = input.apply(Filter.equal(9));
// PCollection will contain [9] at this point
```

Transformarea `Filter` poate fi utilizată atât cu colecții de texte, cât și cu colecții numerice. De exemplu, să încercăm să filtrăm colecția de input care conține **cuvinte**, astfel încât să se returneze doar cuvintele care încep cu litera '`a`'.

Poți, de asemenea, să înlănțuiești mai multe transformări de filtrare pentru a forma filtre mai complexe pe baza mai multor filtre simple sau să implementezi o logică de filtrare mai complexă într-o singură transformare de filtrare. De exemplu, încearcă ambele abordări pentru a filtra aceeași listă de cuvinte astfel încât să se returneze doar cele care încep cu litera '`a`' (indiferent de caz) și care conțin mai mult de trei simboluri.

Sfat: Poți utiliza următorul fragment de cod pentru a crea o PCollection de intrare:

```java
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.values.TypeDescriptor;
import org.apache.beam.sdk.values.TypeDescriptors;
import org.apache.beam.sdk.transforms.Create;
import org.apache.beam.sdk.transforms.Filter;

public class Main {
    public static void main(String[] args) {
        // Creează instanța de Pipeline
        Pipeline pipeline = Pipeline.create();

        // Creează o PCollection de intrare
        PCollection<String> input = pipeline.apply(Create.of(Arrays.asList("Arm", "Andra", "Alin", "Bogdan", "Marius")));

        // Aplică transformarea și obține PCollection de ieșire
        PCollection<String> output = applyTransform(input);

        // Rulează pipeline-ul
        pipeline.run();
    }

    // Metoda pentru aplicarea transformării
    static PCollection<String> applyTransform(PCollection<String> input) {
        return input.apply(Filter.by(word -> word.toLowerCase().charAt(0) == 'a'));
    }
}


```

Output:

```java
["Arm", "Andra", "Alin"]
```



```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.*;
import org.apache.beam.sdk.values.PCollection;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;


public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        // Create input PCollection
        PCollection<Integer> input =
                pipeline.apply(Create.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));

        // The [input] filtered with the applyTransform()
        PCollection<Integer> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<>("PCollection filtered value")));

        pipeline.run();
    }

    // The method filters the collection so that the numbers are even
    static PCollection<Integer> applyTransform(PCollection<Integer> input) {
        return input.apply(Filter.by(number -> number % 2 == 0));
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