# WithKeys in Apache Beam

`WithKeys` primește o PCollection<V> și produce o PCollection<KV<K, V>> asociind fiecare element de input cu o cheie. Există două versiuni ale funcției `WithKeys`, în funcție de modul în care trebuie determinată cheia:

`WithKeys.of(SerializableFunction<V, K> fn)` primește o funcție pentru a calcula cheia pentru fiecare valoare.

```java
PCollection<String> input = pipeline.apply(Create.of("Hello", "World", "Apache", "Beam"));
PCollection<KV<Integer, String>> lengthAndWord = input.apply(WithKeys.of(new SerializableFunction<String, Integer>() {
    @Override
    public Integer apply(String word) {
        return word.length();
    }
}));
```

Output:

```java
KV{6, Apache}
KV{5, World}
KV{4, Beam}
KV{5, Hello}
```

`WithKeys.of(K key)` asociază fiecare valoare cu cheia specificată.

```java
PCollection<String> input = pipeline.apply(Create.of("Hello", "World", "Apache", "Beam"));
PCollection<KV<String, String>> specifiedKeyAndWord = input.apply(WithKeys.of("SpecifiedKey"));
```

Output:

```java
KV{SpecifiedKey, Apache}
KV{SpecifiedKey, Hello}
KV{SpecifiedKey, World}
KV{SpecifiedKey, Beam}
```

Datele sunt returnate sub forma unui card cu o cheie, care este prima literă a cuvântului, iar semnificația cheii este cuvântul însuși.

Exemplu complet:

```java
import static org.apache.beam.sdk.values.TypeDescriptors.strings;

import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.*;
import org.apache.beam.sdk.values.KV;
import org.apache.beam.sdk.values.PCollection;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        // Create input PCollection
        PCollection<String> input =
                pipeline.apply(
                        Create.of("apple", "banana", "cherry", "durian", "guava", "melon"));
        // The [words] filtered with the applyTransform()
        PCollection<KV<String, String>> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<KV<String,String>>("PCollection with-keys value")));

        pipeline.run();
    }

    // Thuis method groups the string collection with its first letter
    static PCollection<KV<String, String>> applyTransform(PCollection<String> input) {
        return input
                .apply(WithKeys.<String, String>of(fruit -> fruit.substring(0, 1))
                        .withKeyType(strings()));
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