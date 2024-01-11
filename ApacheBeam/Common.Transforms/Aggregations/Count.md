# Agregarea in Apache Beam

Transformarile de agrare sunt de 5 feluri:
- `Count`
- `Sum`
- `Mean`
- `Min`
- `Max`


Le vom lua pe rand si le vom explica cu exemple.

# Transformarea Count

Transformarea `Count` oferă mai multe opțiuni pentru calcularea numărului de valori dintr-o PCollection, fie global, fie pentru fiecare cheie. Numără elementele în cadrul fiecărei agregări. Transformarea `Count` are trei variante:

1. Numără toate elementele dintr-o PCollection:
   `Count.globally()` numara numărul de elemente din întreaga PCollection. Rezultatul este o colecție cu un singur element.

```java
PCollection<Integer> input = pipeline.apply(Create.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
PCollection<Long> output = input.apply(Count.globally());
```

Output

```java
10
```

2. Numărarea elementelor pentru fiecare cheie:
   `Count.perKey()` numără câte elemente sunt asociate cu fiecare cheie. Ignoră valorile. Colecția rezultată are un rezultat pentru fiecare cheie din colecția de input.


```java
PCollection<KV<String, Integer>> input = pipeline.apply(
Create.of(KV.of("🥕", 3),
KV.of("🥕", 2),
KV.of("🍆", 1),
KV.of("🍅", 4),
KV.of("🍅", 5),
KV.of("🍅", 3)));
PCollection<KV<String, Long>> output = input.apply(Count.perKey());
```


Output:

```java
KV{🥕, 2}
KV{🍅, 3}
KV{🍆, 1}
```

Numărând toate elementele unice, `Count.perElement()` numără de câte ori apare fiecare element în colecția de input. Colecția rezultată este o pereche cheie-valoare, conținând fiecare element unic și numărul de apariții în colecția originală.

```java
PCollection<KV<String, Integer>> input = pipeline.apply(
Create.of(KV.of("🥕", 3),
KV.of("🥕", 2),
KV.of("🍆", 1),
KV.of("🍅", 3),
KV.of("🍅", 5),
KV.of("🍅", 3)));
PCollection<KV<String, Long>> output = input.apply(Count.perElement());
```

Output:

```java
KV{KV{🍅, 3}, 2}
KV{KV{🥕, 2}, 1}
KV{KV{🍆, 1}, 1}
KV{KV{🥕, 3}, 1}
KV{KV{🍅, 5}, 1}
```

 `Count` returnează numărul de elemente din PCollection. Dacă înlocuiți input-ul cu integers input cu `map input`:

```java
PCollection<KV<Integer, Integer>> input = pipeline.apply(
Create.of(KV.of(1, 11),
KV.of(1, 36),
KV.of(2, 91),
KV.of(3, 33),
KV.of(3, 11),
KV.of(4, 33)));
```

Și înlocuiți `Count.globally` cu `Count.perKey`, va genera numerele de numărare în funcție de cheie. Este, de asemenea, necesar să înlocuiți tipul generic:

```java
PCollection<KV<Integer, Integer>> output = applyTransform(input);
```

```java
static PCollection<KV<Integer, Integer>> applyTransform(PCollection<KV<Integer, Integer>> input) {
    return input.apply(Count.globally());
}
```

```java
import java.util.Arrays;
import org.apache.beam.sdk.values.KV;
```

Numărați câte cuvinte sunt repetate folosind `Count.perElement`:

```java
static PCollection<KV<String, Long>> applyTransform(PCollection<String> input) {
    return input.apply(Count.perElement());
}

```

Exemplu complet:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.transforms.*;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.apache.beam.sdk.values.KV;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        // Create input PCollection
        PCollection<Integer> input =
                pipeline.apply(Create.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));

        // The applyTransform() converts [input] to [output]
        PCollection<Long> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<>("Input has elements")));

        pipeline.run();
    }

    // Count.globally() to return the globally count from `PCollection`
    static PCollection<Long> applyTransform(PCollection<Integer> input) {
        return input.apply(Count.globally());
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

