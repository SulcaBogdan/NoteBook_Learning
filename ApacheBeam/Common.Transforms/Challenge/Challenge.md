# Problema

### Cerinta

Îți sunt furnizate datele sub forma unei PCollection create din array-ul prețurilor comenzilor de taxi dintr-un fișier CSV. 

Sarcina ta este să găsești câte comenzi sunt sub 15 dolari și câte sunt egale sau mai mari de 15 dolari. Returnează-le sub forma unei structuri de tip map (cheie-valoare), cu "above" sau "below" ca cheie, iar valoarea este suma totală (sum) a comenzilor - valoarea. Deși există mai multe modalități de a face acest lucru, încearcă să folosești o altă transformare prezentată în acest modul.



```java
import org.apache.beam.sdk.coders.*;
import org.apache.beam.sdk.io.TextIO;
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.options.PipelineOptions;
import org.apache.beam.sdk.options.PipelineOptionsFactory;
import org.apache.beam.sdk.transforms.*;
import org.apache.beam.sdk.values.KV;
import org.apache.beam.sdk.values.PCollection;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.List;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);
    private static final Double FIXED_COST = 15d;
    private static final String ABOVE_KEY = "above";
    private static final String BELOW_KEY = "below";

    public static void main(String[] args) {
        PipelineOptions options = PipelineOptionsFactory.fromArgs(args).create();
        Pipeline pipeline = Pipeline.create(options);

        // Create input PCollection
        PCollection<String> input = pipeline.apply(TextIO.read().from("SulcaBogdan/NoteBook_Learning/ApacheBeam/Common.Transforms/Challenge/sample1000.csv"));

        // Extract cost from PCollection
        PCollection<Double> rideTotalAmounts = input.apply(ParDo.of(new ExtractTaxiRideCostFn()));

        // Filtering with fixed cost
        PCollection<Double> aboveCosts = getAboveCost(rideTotalAmounts);
        PCollection<Double> belowCosts = getBelowCost(rideTotalAmounts);

        // Summing up the price above the fixed price
        PCollection<Double> aboveCostsSum = getSum(aboveCosts, "Sum above cost");

        // Summing up the price below the fixed price
        PCollection<Double> belowCostsSum = getSum(belowCosts, "Sum below cost");

        // Create map[key,value] and output
        PCollection<KV<String,Double>> aboveKV = setKeyForCost(aboveCostsSum, ABOVE_KEY)
                .apply("Log above cost",ParDo.of(new LogOutput<>("Above pCollection output")));

        // Create map[key,value] and output
        PCollection<KV<String,Double>> belowKV = setKeyForCost(belowCostsSum, BELOW_KEY)
                .apply("Log below cost",ParDo.of(new LogOutput<>("Below pCollection output")));


        pipeline.run();
    }

    static PCollection<Double> getSum(PCollection<Double> input, String name) {
        return input.apply(name, Sum.doublesGlobally());
    }

    static PCollection<Double> getAboveCost(PCollection<Double> input) {
        return input.apply("Filter above cost", Filter.by(number -> number >= FIXED_COST));
    }

    static PCollection<Double> getBelowCost(PCollection<Double> input) {
        return input.apply("Filter below cost", Filter.by(number -> number < FIXED_COST));
    }

    static PCollection<KV<String, Double>> setKeyForCost(PCollection<Double> input,String key) {
        return input.apply(WithKeys.of(number -> key)).setCoder(KvCoder.of(StringUtf8Coder.of(),DoubleCoder.of()));
    }

    static class ExtractTaxiRideCostFn extends DoFn<String, Double> {
        @ProcessElement
        public void processElement(ProcessContext c) {
            String[] items = c.element().split(",");
            Double totalAmount = tryParseTaxiRideCost(items);
            c.output(totalAmount);
        }
    }

    private static String tryParseString(String[] inputItems, int index) {
        return inputItems.length > index ? inputItems[index] : null;
    }

    private static Double tryParseTaxiRideCost(String[] inputItems) {
        try {
            return Double.parseDouble(tryParseString(inputItems, 16));
        } catch (NumberFormatException | NullPointerException e) {
            return 0.0;
        }
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