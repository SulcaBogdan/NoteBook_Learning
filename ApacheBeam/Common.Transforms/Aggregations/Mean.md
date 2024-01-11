# Transformarea Mean in Apache Beam

Puteți utiliza transformările `Mean` pentru a calcula media aritmetică a elementelor dintr-o colecție sau media valorilor asociate cu fiecare cheie într-o colecție de perechi cheie-valoare. `Mean.globally()` returnează o transformare care furnizează o colecție al cărei conținut este media elementelor colecției de input. Dacă nu există elemente în colecția de input, se returnează `0`.

```java
PCollection<Integer> input = pipeline.apply(Create.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
PCollection<Double> mean = input.apply(Mean.globally());
```

Output:

```java
5.5
```

`Mean.perKey()` returnează o transformare care furnizează o colecție conținând un element de ieșire care mapează fiecare cheie distinctă din colecția de input la media valorilor asociate cu acea cheie în colecția de input.

```java
PCollection<KV<String, Integer>> input = pipeline.apply(
Create.of(KV.of("🥕", 3),
KV.of("🥕", 2),
KV.of("🍆", 1),
KV.of("🍅", 4),
KV.of("🍅", 5),
KV.of("🍅", 3)));
PCollection<KV<String, Double>> meanPerKey = input.apply(Mean.perKey());
```

Output:

```java
KV{🍆, 1.0}
KV{🥕, 2.5}
KV{🍅, 4.0}
```

`Mean.globally` returnează media aritmetică din PCollection. Dacă înlocuiți input-ul cu această `map inputs` :

```java
PCollection<KV<Integer, Integer>> input = pipeline.apply(
Create.of(KV.of(1, 11),
KV.of(1, 36),
KV.of(2, 91),
KV.of(3, 33),
KV.of(3, 11),
KV.of(4, 33)));
```

Și înlocuiți `Mean.globally` cu `Mean.perKey`, va genera media în funcție de cheie. Este, de asemenea, necesar să înlocuiți tipul generic:

```java
PCollection<KV<Integer, Double>> output = applyTransform(input);
```

```java
static PCollection<KV<Integer, Double>> applyTransform(PCollection<KV<Integer, Integer>> input) {
    return input.apply(Mean.perKey());
}
```


Exemplu complet:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.*;
import org.apache.beam.sdk.values.PCollection;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.apache.beam.sdk.values.KV;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        // Create input PCollection
        PCollection<Integer> input = pipeline.apply(Create.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));

        // The applyTransform() converts [input] to [output]
        PCollection<Double> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<>("PCollection mean value")));

        pipeline.run();
    }

    // Mean.globally() to return the globally mean from `PCollection`
    static PCollection<Double> applyTransform(PCollection<Integer> input) {
        return input.apply(Mean.globally());
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
```output:
The results of this example are taken from the Apache Beam Playground cache.
Jun 27, 2023 10:32:14 AM Task$LogOutput processElement
INFO: PCollection mean value: 5.5
```

