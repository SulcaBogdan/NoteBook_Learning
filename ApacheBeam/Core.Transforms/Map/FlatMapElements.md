# FlatMapElements in Apache Beam

Funcționează asemănător cu `MapElements`, dar în interiorul logicii poți efectua operații complexe, cum ar fi divizarea listei în elemente separate și procesarea acestora.

```java
static PCollection<String> applyTransform(PCollection<String> input) {
        return input.apply(
                FlatMapElements.into(TypeDescriptors.strings())
                        .via(sentence -> Arrays.asList(sentence.split(" ")))
        );
    }
```

Exemplu complet:

```java
import java.util.Arrays;
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.*;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.values.TypeDescriptors;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);
        
        // List of elements
        PCollection<String> input =
                pipeline.apply(Create.of("Apache Beam", "Unified Batch and Streaming"));

        // The applyTransform() converts [sentences] to [output]
        PCollection<String> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<String>()));

        pipeline.run();
    }
// The method returns a list of converted strings in sentences
    static PCollection<String> applyTransform(PCollection<String> input) {
        return input.apply(
                FlatMapElements.into(TypeDescriptors.strings())
                        .via(sentence -> Arrays.asList(sentence.split(" ")))
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
