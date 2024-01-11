# Transformarea Max in Apache Beam

`Max` provides a variety of different transforms for computing the maximum values in a collection, either globally or for each key.

You can find the global maximum value from the PCollection by using `Max.doublesGlobally()`

```java
PCollection<Integer> input = pipeline.apply(Create.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
PCollection<Double> max = input.apply(Max.doublesGlobally());
```
Output:

```java
10
```

Puteți utiliza `Max.integersPerKey()` pentru a calcula valoarea maximă întreagă asociată cu fiecare cheie unică (de tip String).

```java
PCollection<KV<String, Integer>> input = pipeline.apply(
Create.of(KV.of("🥕", 3),
KV.of("🥕", 2),
KV.of("🍆", 1),
KV.of("🍅", 4),
KV.of("🍅", 5),
KV.of("🍅", 3)));

PCollection<KV<String, Integer>> maxPerKey = input.apply(Max.integersPerKey());
```

Output:

```java
KV{🍅, 5}
KV{🥕, 3}
KV{🍆, 1}
```

`Max.doublesGlobally` returnează elementul maxim din `PCollection`. Dacă înlocuiți input-ul cu aceast `map input`:

```java
PCollection<KV<Integer, Integer>> input = pipeline.apply(
Create.of(KV.of(1, 11),
KV.of(1, 36),
KV.of(2, 91),
KV.of(3, 33),
KV.of(3, 11),
KV.of(4, 33)));
```

Și înlocuiți `Max.doublesGlobally` cu `Max.integersPerKey`, va genera numerele maxime în funcție de cheie. Este, de asemenea, necesar să înlocuiți tipul generic:

```java
PCollection<KV<Integer, Integer>> output = applyTransform(input);
```

```java
static PCollection<KV<Integer, Integer>> applyTransform(PCollection<KV<Integer, Integer>> input) {
        return input.apply(Max.integersPerKey());
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
        PCollection<Integer> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<>("PCollection maximum value")));

        pipeline.run();
    }

    // Max.integersGlobally() to return the globally maximum from `PCollection`
    static PCollection<Integer> applyTransform(PCollection<Integer> input) {
        return input.apply(Max.integersGlobally());
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

Output:

```java
The results of this example are taken from the Apache Beam Playground cache.
Jun 27, 2023 10:32:10 AM Task$LogOutput processElement
INFO: PCollection maximum value: 10
```

