# MapElements in Apache Beam


Dacă funcția dvs. este relativ simplă, puteți simplifica utilizarea `ParDo` oferind un `DoFn` încorporat ușor ca instanță anonimă a clasei interne.

```java
PCollection<String> input = ...;

// Apply a ParDo with an anonymous DoFn to the PCollection [input].
// Save the result as the PCollection wordLengths.
PCollection<Integer> wordLengths = input.apply(
"ComputeWordLengths", // the transform name
ParDo.of(new DoFn<String, Integer>() { // a DoFn as an anonymous inner class instance
@ProcessElement
public void processElement(@Element String word, OutputReceiver<Integer> out) {
out.output(word.length());
}
}));
```
Dacă `ParDo` efectuează o mapare one-to-one a elementelor input la elementele output – adică pentru fiecare element input, aplică o funcție care produce exact un element output, puteți utiliza transformarea `MapElements` de nivel superior.

`MapElements` poate accepta o funcție `lambda Java 8 anonimă `pentru o concizie suplimentară. Iată exemplul anterior folosind `MapElements`:

```java
// The input PCollection.
PCollection<String> input = ...;

// Apply a MapElements with an anonymous lambda function to the PCollection [input].
// Save the result as the PCollection wordLengths.
PCollection<Integer> wordLengths = input.apply(
MapElements.into(TypeDescriptors.integers())
.via((String word) -> word.length()));
```

Exemplu complet:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.values.TypeDescriptors;
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
                pipeline.apply(Create.of(10, 20, 30, 40, 50));

        // The applyTransform() converts [input] to [output]
        PCollection<Integer> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<Integer>()));

           pipeline.run();
    }

    // The method returns the value of `PCollection' multiplied by 5
    static PCollection<Integer> applyTransform(PCollection<Integer> input) {
        return input.apply(
                MapElements.into(TypeDescriptors.integers())
                        .via(number -> number * 5)
        );
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