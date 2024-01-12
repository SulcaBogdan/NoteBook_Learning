# ParDo one-to-many

Funcționează ca `ParDo one-to-one`, dar în interiorul logicii puteți face operațiuni complexe, cum ar fi împărțirea listei în elemente separate și procesarea.

```java
static PCollection<String> applyTransform(PCollection<String> input) {
        return input.apply(ParDo.of(new DoFn<String, String>() {
            @ProcessElement
            public void processElement(@Element String sentence, OutputReceiver<String> out) {
                // Divided sentences into words
                String[] words = sentence.split(" ");

                // Operations on each element
                for (String word : words) {
                    out.output(word);
                }
            }

        }));
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

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

// List of elements
        PCollection<String> input =
                pipeline.apply(Create.of("Hello Beam", "It is awesome"));

        // The applyTransform() converts [sentences] to [output]
        PCollection<String> output = applyTransform(input);

        output.apply("Log", ParDo.of(new LogOutput<String>()));


        pipeline.run();
    }

    // The applyTransform() divides a sentence into an array of words and outputs each word
    static PCollection<String> applyTransform(PCollection<String> input) {
        return input.apply(ParDo.of(new DoFn<String, String>() {
            @ProcessElement
            public void processElement(@Element String sentence, OutputReceiver<String> out) {
                String[] words = sentence.split(" ");

                for (String word : words) {
                    out.output(word);
                }
            }

        }));
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