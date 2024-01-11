# Transformarea Sum in Apache Beam

Puteți utiliza transformările `Sum` pentru a calcula suma elementelor dintr-o colecție sau suma valorilor asociate cu fiecare cheie într-o colecție de perechi cheie-valoare. Puteți găsi valoarea globală a sumei din PCollection folosind `Sum.doublesGlobally()`.

```java
PCollection<Integer> input = pipeline.apply(Create.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
PCollection<Double> sum = input.apply(Sum.doublesGlobally());
```

Output:

```java
55
```

Puteți utiliza `Sum.integersPerKey()` pentru a calcula suma a valorilor întregi asociate cu fiecare cheie unică (care este de tip String).

```java
PCollection<KV<String, Integer>> input = pipeline.apply(
Create.of(KV.of("🥕", 3),
KV.of("🥕", 2),
KV.of("🍆", 1),
KV.of("🍅", 4),
KV.of("🍅", 5),
KV.of("🍅", 3)));
PCollection<KV<String, Integer>> sumPerKey = input.apply(Sum.integersPerKey());
```
Output:

```java
KV{🍆, 1}
KV{🍅, 12}
KV{🥕, 5}
```

Puteți utiliza `Sum()` pentru a aduna elementele unei PCollection. `Sum.integersGlobally` returnează suma din PCollection. Dacă înlocuiți input-ul cu această `map input`:

```java
PCollection<KV<Integer, Integer>> input = pipeline.apply(
    Create.of(KV.of(1, 11),
    KV.of(1, 36),
    KV.of(2, 91),
    KV.of(3, 33),
    KV.of(3, 11),
    KV.of(4, 33)));
```

Și înlocuiți `Sum.integersGlobally` cu `Sum.integersPerKey`, va genera suma în funcție de cheie. Este, de asemenea, necesar să înlocuiți tipul generic:

```java
PCollection<KV<Integer, Integer>> output = applyTransform(input);
```

```java
static PCollection<KV<Integer, Integer>> applyTransform(PCollection<KV<Integer, Integer>> input) {
        return input.apply(Sum.integersPerKey());
    }
```

Exemplu:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.values.PCollection;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.apache.beam.sdk.transforms.*;
import org.apache.beam.sdk.values.KV;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        // Create input PCollection
        PCollection<Integer> input = pipeline.apply(Create.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));

        // The applyTransform() converts [input] to [output]
        PCollection<Integer> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<>("PCollection sum value")));

        pipeline.run();
    }

    // Sum.integersGlobally() to return the globally sum from `PCollection`
    static PCollection<Integer> applyTransform(PCollection<Integer> input) {
        return input.apply(Sum.integersGlobally());
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