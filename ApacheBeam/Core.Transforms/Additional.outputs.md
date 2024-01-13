# Additional Outputs in Apache Beam


În timp ce `ParDo` returnează întotdeauna output-ul principal a PCollection (ca valoare de returnare din aplicare), puteți forța `ParDo` să returneze și oricâte alte output-uri PCollection doriți. Dacă decideți să aveți mai multe output-uri, ParDo-ul dumneavoastră va returna toate output-urile PCollection (inclusiv output-ul principal) combinate. Aceasta va fi util atunci când lucrați cu date mari sau o bază de date care trebuie împărțită în diferite colecții. Când primiți un `PCollectionTuple` combinat, puteți folosi `TupleTag` pentru a obține o PCollection.

Un `PCollectionTuple` este o tuplă imutabilă de PCollection-uri cu tipuri heterogene, etichetate cu "keys" `TupleTag`. Un `PCollectionTuple` poate fi folosit ca input sau output pentru un `PTransform` care primește sau creează mai multe input-uri sau output-uri PCollection, care pot fi de tipuri diferite, de exemplu, ParDo cu mai multe output-uri.

Un `TupleTag` este o etichetă tipizată folosită ca cheie a unei tuple cu tipuri heterogene, cum ar fi `PCollectionTuple`. Parametrul său de tip general vă permite să urmăriți tipul static al elementelor stocate în tuple.

```java
ParDo.of(new DoFn<String, String>() {
     public void processElement(@Element String word, MultiOutputReceiver out) {
       if (word.length() <= wordLengthCutOff) {
         // Emit short word to the main output.
         // In this example, it is the output with tag wordsBelowCutOffTag.
         out.get(wordsBelowCutOffTag).output(word);
       } else {
         // Emit long word length to the output with tag wordLengthsAboveCutOffTag.
         out.get(wordLengthsAboveCutOffTag).output(word.length());
       }
       if (word.startsWith("MARKER")) {
         // Emit word to the output with tag markedWordsTag.
         out.get(markedWordsTag).output(word);
       }
     }})).withOutputTags(wordsBelowCutOffTag,
          // Specify the tags for the two additional outputs as a TupleTagList.
                          TupleTagList.of(wordLengthsAboveCutOffTag).and(markedWordsTag)));
```

Exempu complet:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.*;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.values.PCollectionTuple;
import org.apache.beam.sdk.values.TupleTag;
import org.apache.beam.sdk.values.TupleTagList;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import java.util.Arrays;
import org.apache.beam.sdk.values.TypeDescriptors;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        // List of elements
        PCollection<Integer> input = pipeline.apply(Create.of(10, 50, 120, 20, 200, 0));

        TupleTag<Integer> numBelow100Tag = new TupleTag<Integer>() {};
        TupleTag<Integer> numAbove100Tag = new TupleTag<Integer>() {};

        // The applyTransform() converts [input] to [outputTuple]
        PCollectionTuple outputTuple = applyTransform(input, numBelow100Tag, numAbove100Tag);

        outputTuple.get(numBelow100Tag).apply("Log Number <= 100: ", ParDo.of(new LogOutput<Integer>("Number <= 100: ")));

        outputTuple.get(numAbove100Tag).apply("Log Number > 100: ", ParDo.of(new LogOutput<Integer>("Number > 100: ")));


        pipeline.run();  
    }
    // The function has multiple outputs, numbers above 100 and below
    static PCollectionTuple applyTransform(
            PCollection<Integer> input, TupleTag<Integer> numBelow100Tag,
            TupleTag<Integer> numAbove100Tag) {

        return input.apply(ParDo.of(new DoFn<Integer, Integer>() {

            @ProcessElement
            public void processElement(@Element Integer number, MultiOutputReceiver out) {
                if (number <= 100) {
                    // First PCollection
                    out.get(numBelow100Tag).output(number);
                } else {
                    // Additional PCollection
                    out.get(numAbove100Tag).output(number);
                }
            }

        }).withOutputTags(numBelow100Tag, TupleTagList.of(numAbove100Tag)));
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