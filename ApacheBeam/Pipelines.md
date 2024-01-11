# Pipelines in Apache Beam

Pentru a utiliza Beam, trebuie să creezi mai întâi un program de conducere folosind clasele dintr-unul dintre SDK-urile Beam. Programul tău de conducere definește `pipeline`-ul tău, inclusiv toate `inputs`, `transforms` și `outputs`. De asemenea, stabilește opțiunile de execuție pentru `pipeline`, de obicei, transmise prin opțiuni de linie de comandă. Aceste opțiuni includ Runner-ul de pipeline, care, la rândul său, determină platforma pe care va pipeline-ul tau.

SDK-urile Beam furnizează mai multe abstractizări care simplifică mecanica prelucrării de date distribuite la scară largă. Aceste abstractizări funcționează atât `batch`, cât și `streaming`. Atunci când creezi pipeline-ul Beam, poți conceptualiza task-ul ta de procesare a datelor în funcție de aceste abstractizări. Acestea includ:


1. `Pipeline`: Un `Pipeline` încapsulează întreaga ta sarcină de prelucrare a datelor, de la început până la sfârșit. Acest lucru include citirea datelor `input`, transformarea acestor date și scrierea datelor in `output`. Toate programele de conducere Beam trebuie să creeze un `Pipeline`. Atunci când creezi Pipeline-ul, trebuie să specifici și `run options` care îi spun Pipeline-ului unde și cum să ruleze.

2. `PCollection`: Un `PCollection` reprezintă un set de date distribuit asupra căruia lucrează pipeline-ul Beam. Setul de date poate fi `bounded`, ceea ce înseamnă că provine de la o sursă `fixă`(de exemplu un text document sau csv), cum ar fi un, sau `unbounded`, ceea ce înseamnă că provine de la o sursă în curs de actualizare continuă printr-o abonare sau alt mecanism. Pipeline-ul tau creează în mod obișnuit un `PCollection` inițial citind date dintr-o sursă externă de date, dar poți crea, de asemenea, un `PCollection` din date în memorie în cadrul programului tău. De acolo, `PCollections` sunt input-utirile și output-urile pentru fiecare pas în pipeline-ul tau.

3. `PTransform`: Un `PTransform` reprezintă o operație de prelucrare a datelor sau un pas in `pipeline`. Fiecare `PTransform` ia unul sau mai multe obiecte `PCollection` ca **input**, efectuează o funcție de procesare pe elementele acelei `PCollection` pe care o furnizezi, și apoi produce zero sau mai multe obiecte `PCollection` de `output`.

4. `Transformări` I/O: Beam vine cu mai multe "IO-uri" - Transformări `P` din bibliotecă care citesc sau scriu date în diverse sisteme de stocare externe.

Un program tipic Beam funcționează astfel:

1. Creează un obiect `Pipeline` și setează opțiunile de execuție ale pipeline-ului, inclusiv Runner-ul de `Pipeline`.

2. Creează un PCollection inițial pentru datele fluxului, fie folosind IO-urile pentru a citi datele dintr-un sistem de stocare extern, fie folosind o transformare `Create` pentru a construi un `PCollection` din date în memorie.

3. Aplică `Transformări` la fiecare `PCollection`. `Transformările` pot **modifica**, **filtra**, **grupa**, **analiza** sau **prelucra** în alt mod elementele dintr-un PCollection. O transformare *creează un nou PCollection* de `output` fără a modifica datele din `input`. Un pipeline tipic aplică transformări ulterioare la fiecare nou PCollection  de output pe rând până când prelucrarea este completă. Cu toate acestea, reține că un pipeline nu trebuie să fie o linie dreaptă unică de transformări aplicate una după alta: gândește-te la `PCollections` ca la `variabile` și la `PTransforms` ca la `funcții` aplicate acestor variabile: forma pipeline-ului poate fi un graf de prelucrare arbitrabil de complex.

4. Folosește IO-urile pentru a scrie `PCollection`(s) final(e), transformate, într-o sursă externă.

5. Rulează fluxul de lucru folosind `Runner`-ul de Pipeline desemnat.

Când rulezi programul tău Beam, Runner-ul de Pipeline pe care îl desemnezi construiește un `workflow graph` al pipeline-ului bazat pe obiectele `PCollection` pe care le-ai creat și transformările pe care le-ai aplicat. Acest `graph` este apoi executat folosind platforma de prelucrare distribuită corespunzătoare, devenind un "`job`" asincron pe acea platformă.



# Crearea unui Pipeline

`Pipeline` încapsulează toate datele și pașii din task-ul tau de prelucrare a datelor. Programul tău Beam începe în mod tipic prin construirea unui obiect `Pipeline` și apoi folosește acel obiect ca bază pentru crearea seturilor de date ale pipeline-ului ca `PCollections` și a operațiilor sale ca `Transformări`.

Pentru a utiliza Beam, programul tău trebuie să creeze mai întâi o instanță a clasei Pipeline din SDK-ul Beam (în mod obișnuit, în funcția `main()`). La crearea Pipeline-ului, va trebui să setezi și câteva opțiuni de configurare. Puteți seta opțiunile de configurare ale pipeline-ului în mod programatic, dar adesea este mai ușor să setezi opțiunile în avans (sau să le citești de la linia de comandă) și să le transmiți obiectului `Pipeline` când creezi obiectul.

```java
// Start by defining the options for the pipeline.
PipelineOptions options = PipelineOptionsFactory.create();

// Then create the pipeline.
Pipeline pipeline = Pipeline.create(options);
```
Când creezi pipeline-ul și scrii argumente într-un program (prin intermediul parametrului `String args[]`), poți specifica explicit runner-ul pe care vrei să-l utilizezi.

```bash
--runner=DirectRunner
```

## Exemplu de pipeline in Java

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

        PCollection<String> output = createPCollection(pipeline);

        output.apply("Log", ParDo.of(new LogOutput<String>()));

        pipeline.run();
    }

    static PCollection<String> createPCollection(Pipeline pipeline) {
        return pipeline.apply(Create.of("Hello Beam"));
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

```bash
The results of this example are taken from the Apache Beam Playground cache.
Jun 27, 2023 10:35:17 AM Task$LogOutput processElement
INFO: Processing element: Hello Beam
```

# Configurarea Pipeline Options

Folosește opțiunile de pipeline pentru a configura diferite aspecte ale pipeline-ului, cum ar fi runner-ul de pipeline care va executa pipeline-ul și orice configurație specifică runner-ului necesară pentru runner-ul ales. Opțiunile de pipeline pot include informații precum ID-ul proiectului sau o locație pentru stocarea fișierelor.

Când rulezi pipeline-ul pe un runner ales, o copie a `PipelineOptions` va fi disponibilă în codul tău. De exemplu, dacă adaugi un parametru `PipelineOptions` în metoda `@ProcessElement` a unui `DoFn`, acesta va fi populat de sistem.

Configurarea `PipelineOptions` din argumente de linie de comandă

Deși poți configura pipeline-ul prin crearea unui obiect `PipelineOptions` și setarea directă a câmpurilor acestuia, SDK-urile Beam includ un `command-line parser` pe care îl poți utiliza pentru a seta câmpuri în `PipelineOptions` folosind argumente de command-line.

Pentru a citi opțiuni de la command-line, construiește obiectul `PipelineOptions` așa cum este demonstrat în următorul cod exemplu:

```java
PipelineOptions options = PipelineOptionsFactory.fromArgs(args).withValidation().create();
```

Aceasta interpretează argumente de command-line care urmează formatul:

```bash
--<option>=<value>
```

**Adăugarea metodei `.withValidation` va verifica argumentele necesare de command-line și va valida valorile argumentelor.**

### Crearea de opțiuni personalizate

Poți adăuga propriile opțiuni personalizate în plus față de opțiunile standard ale `PipelineOptions`. Exemplul următor arată cum să adaugi opțiuni personalizate de `input` și `output`:

Pentru a adăuga propriile opțiuni, definește o interfață cu metode de obținere și stabilire pentru fiecare opțiune.

```java
public interface MyOptions extends PipelineOptions {
    String getInput();
    void setInput(String input);

    String getOutput();
    void setOutput(String output);
}
```

Setezi descrierea și valoarea implicită folosind `adnotări`, astfel:

```java
public interface MyOptions extends PipelineOptions {
    @Description("Input for the pipeline")
    @Default.String("gs://my-bucket/input")
    String getInput();
    void setInput(String input);

    @Description("Output for the pipeline")
    @Default.String("gs://my-bucket/output")
    String getOutput();
    void setOutput(String output);
}
```

Se recomandă să înregistrezi interfața ta cu `PipelineOptionsFactory` și apoi să o furnizezi când creezi obiectul `PipelineOptions`. Atunci când înregistrezi interfața ta cu `PipelineOptionsFactory`, opțiunea `--help` poate găsi interfața opțiunilor personalizate și o adaugă la ieșirea comenzii `--help`. De asemenea, `PipelineOptionsFactory` va valida că opțiunile tale personalizate sunt compatibile cu toate celelalte opțiuni înregistrate.

Exemplul următor arată cum să înregistrezi interfața ta de opțiuni personalizate cu `PipelineOptionsFactory`:

```java
PipelineOptionsFactory.register(MyOptions.class);
MyOptions options = PipelineOptionsFactory.fromArgs(args).withValidation().as(MyOptions.class);
```

## Exercitiu

Puteți găsi codul complet al exemplului de mai sus în fereastra de joacă, pe care o puteți rula și experimenta cu ea. 

Puteți transfera fișiere cu alte extensii. De exemplu, un fișier CSV cu date despre comenzi de taxi. După efectuarea unor transformări, puteți scrie într-un nou fișier CSV. 


Iată o mică listă de câmpuri și un exemplu de înregistrare din acest set de date:

| cost | passenger_count | ... |
|------|------------------|-----|
| 5.81 | 4.62             | ... |
| 4.6  | 2                | ... |
| 24   | 1                | ... |

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.io.TextIO;
import org.apache.beam.sdk.options.*;
import org.apache.beam.sdk.values.PCollection;
import org.apache.beam.sdk.transforms.*;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Task {

    private static final Logger LOG = LoggerFactory.getLogger(Task.class);

    public interface MyOptions extends PipelineOptions {
        // Default value if [--output] equal null
        @Description("Path of the file to read from")
        @Default.String("gs://apache-beam-samples/shakespeare/kinglear.txt")
        String getInputFile();


        void setInputFile(String value);


        // Set this required option to specify where to write the output.
        @Description("Path of the file to write to")
        @Validation.Required
        String getOutput();

        void setOutput(String value);
    }

    public static void main(String[] args) {
        MyOptions options = PipelineOptionsFactory.fromArgs(args).withValidation().as(MyOptions.class);

        readLines(options);

    }

    static void readLines(MyOptions options) {
        Pipeline pipeline = Pipeline.create(options);
        PCollection<String> output = pipeline.apply("ReadLines", TextIO.read().from(options.getInputFile()))
                .apply(Filter.by((String line) -> !line.isEmpty()));

        output.apply("Log", ParDo.of(new LogOutput<String>()));
        pipeline.run().waitUntilFinish();
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

