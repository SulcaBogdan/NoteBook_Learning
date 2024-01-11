# Conceptele Apache Beam


**Apache Beam** furnizează un strat portabil de API pentru construirea `pipelines`, care pot fi executate pe o varietate de engine-uri sau "`runners`". Conceptele de bază ale acestui strat se bazează pe **Modelul Beam** (cunoscut anterior sub numele de **Modelul Dataflow**) și sunt implementate în diverse grade în fiecare `runner` Beam.

### Direct Runner

**`Direct Runner`** execută pipelines pe mașina ta și este proiectat pentru a valida că acestea respectă cât mai strâns modelul Apache Beam. În loc să se concentreze pe execuția eficientă a pipeline-ului, `Direct Runner` efectuează verificări suplimentare pentru a asigura că utilizatorii nu se bazează pe semantici care nu sunt garantate de model. Unele dintre aceste verificări includ:

- impunerea imutabilității elementelor
- impunerea posibilității de a fi codate a elementelor
- elementele sunt procesate într-o ordine arbitrară în toate punctele
- serializarea funcțiilor utilizatorului (`DoFn`, `CombineFn`, etc.)

Utilizarea `Direct Runner` pentru testare și dezvoltare ajută la asigura ca pipeline-urile sunt eficiente în diverse runners Beam. În plus, depanarea execuțiilor eșuate poate fi un `task non-practic` atunci când un pipeline este executat pe un **cluster** remote. În schimb, este adesea mai rapid și mai simplu să efectuați unit teste locale pentru codul pipeline-ului. **Unit testing** local vă permite, de asemenea, să utilizați instrumentele preferate de **debug** locale.

## Specificati depententa

Atunci când folosești Java, trebuie să specifici dependența ta de `Direct Runner` în fișierul `pom.xml`.

```xml
<dependency>
    <groupId>org.apache.beam</groupId>
    <artifactId>beam-runners-direct-java</artifactId>
    <version><!-- Specifică versiunea dorită --></version>
</dependency>
```

## Seteaza runner-ul

În Java, trebuie să setezi runner-ul în `args` atunci când începi programul.

```bash
--runner=DirectRunner
```

Argumentul `--runner=DirectRunner` se specifică în linia de comandă atunci când rulezi programul Java care conține un pipeline Apache Beam. De obicei, este adăugat la sfârșitul comenzii de execuție a programului.

```bash
java -cp NumeFisier.jar NumeClasaProgram --runner=DirectRunner
```

## **Google Cloud Dataflow Runner**

`Google Cloud Dataflow` utilizează serviciul gestionat `Cloud Dataflow`. Atunci când rulezi `pipeline`-ul tău cu serviciul `Cloud Dataflow`, runner-ul încarcă codul tău executabil și dependentele într-un `bucket Google Cloud Storage` și creează un `job` Cloud Dataflow, care execută pipeline-ul tău pe resurse gestionate în Google Cloud Platform. Runner-ul și serviciul Cloud Dataflow sunt potrivite pentru job-uri de scară mare, continue, și oferă:

- **Un serviciu complet gestionat**
- **Autoscalare a numărului de workers pe toată durata job-ului**
- **Reechilibrare dinamică a task-urilor de lucru**

## Exemplu Run

Când utilizați Java, trebuie să specificați dependența dvs. de `Cloud Dataflow Runner` în `pom.xml`.

```xml
<dependency>
<groupId>org.apache.beam</groupId>
<artifactId>beam-runners-google-cloud-dataflow-java</artifactId>
<version>2.42.0</version>
<scope>runtime</scope>
</dependency>
```

Apoi, adauga numele clasei `Main` in `Maven JAR plugin`.

```xml
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-jar-plugin</artifactId>
<version>${maven-jar-plugin.version}</version>
<configuration>
<archive>
<manifest>
<addClasspath>true</addClasspath>
<classpathPrefix>lib/</classpathPrefix>
<mainClass>NUMELE_CLASEI_TALE</mainClass>
</manifest>
</archive>
</configuration>
</plugin>
```

**Consola:**

```java -jar target/beam-examples-bundled-1.0.0.jar \
--runner=DataflowRunner \
--project=<YOUR_GCP_PROJECT_ID> \
--region=<GCP_REGION> \
--tempLocation=gs://<YOUR_GCS_BUCKET>/temp/
```

## **Apache Flink Runner**

`Apache Flink Runner` poate fi folosit pentru a executa pipeline-uri  Beam utilizând `Apache Flink`. Pentru execuție, poți alege între un mod de execuție în `cluster` (de exemplu, `Yarn/Kubernetes/Mesos`) sau un mod de execuție local integrat, util pentru testarea pipeline-urilor. `Flink Runner` și `Flink` sunt potrivite pentru job-uri continue la scară mare și oferă:

- **Un runtime axat pe `streaming` care suportă atât procesarea `batch` cât și programele de streaming de date**
- **Un runtime care susține un `throughput` foarte mare și o latenta scăzută a evenimentelor în același timp**
- **Toleranță la defecte cu garanții de procesare `exactly-once`**
- **Presiune naturală în programele de `streaming`**
- **Gestionarea personalizată a memoriei pentru o schimbare eficientă și robustă între algoritmi de procesare a datelor în memorie și în afara acesteia**
- **Integrare cu `YARN` și alte componente ale ecosistemului `Apache Hadoop`**

## Exemplu Run

**Portabil**

1. Începând cu Beam 2.18.0, imagini Docker pre-compile ale serviciului de job Flink sunt disponibile pe Docker Hub pentru versiunile` Flink 1.10`, `Flink 1.11`, `Flink 1.12`, `Flink 1.13` și `Flink 1.14.2`.

2. Porniți endpoint-ul JobService:
```bash
docker run --net=host apache/beam_flink1.10_job_server:latest
```
3. Trimiteți pipeline-ul către endpoint-ul de mai sus, folosind `PortableRunner`, cu `job_endpoint` setat la `localhost:8099` (aceasta este adresa implicită a `JobService`). Opțional, setați `environment_type` la `LOOPBACK`. De exemplu:

```python
import apache_beam as beam
from apache_beam.options.pipeline_options import PipelineOptions

options = PipelineOptions([
    "--runner=PortableRunner",
    "--job_endpoint=localhost:8099",
    "--environment_type=LOOPBACK"
])
with beam.Pipeline(options) as p:
...
```

**Non-portabil**

Atunci când folosești Java, trebuie să specifici dependența de Cloud Dataflow Runner în fișierul `pom.xml`.

```xml
<dependency>
  <groupId>org.apache.beam</groupId>
  <artifactId>beam-runners-flink-1.14</artifactId>
  <version>2.42.0</version>
</dependency>
```

**Consola:**

```bash
mvn exec:java -Dexec.mainClass=org.apache.beam.examples.WordCount \
-Pflink-runner \
-Dexec.args="--runner=FlinkRunner \
--inputFile=/path/to/pom.xml \
--output=/path/to/counts \
--flinkMaster=<flink master url> \
--filesToStage=target/word-count-beam-bundled-0.1.jar"
```


**Apache Spark Runner**

`Apache Spark Runner` poate fi utilizat pentru a executa pipeline-uri Beam folosind `Apache Spark`. Acest `Runner` poate executa pipeline-uri Spark exact ca o aplicație Spark nativă; implementând o aplicație autonomă pentru modul local, care rulează pe `ResourceManager`-ul Standalone al Spark, sau utilizând `YARN` sau `Mesos`. Apache Spark Runner execută pipeline-urile Beam pe Apache Spark, oferind:

- **Fluxuri de date atât pentru procesare în lot, cât și pentru programe de streaming (și combinate).**
- **Aceleași garanții de toleranță la defecte oferite de RDD-uri și DStreams.**
- **Aceleași caracteristici de securitate furnizate de Spark.**
- **Raportarea incorporată a metricilor folosind sistemul de metrici al Spark, care raportează Aggregator-urile Beam.**
- **Suport nativ pentru intrările secundare Beam prin variabilele de tip Broadcast ale Spark.**

De asemenea, poți citi mai multe despre Apache Spark Runner aici:
1. Cu Docker (preferat): 
```bash
  docker run --net=host apache/beam_spark_job_server:latest
```

2. Trimiteți fluxul de lucru Python către endpoint-ul de mai sus, utilizând `PortableRunner`, cu `job_endpoint` setat la `localhost:8099` (aceasta este adresa implicită a `JobService`), și `environment_type` setat la `LOOPBACK`. De exemplu:

```bash
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.WordCount \
-Dexec.args="--runner=SparkRunner --inputFile=pom.xml --output=counts" -Pspark-runner
```

**Non-portable**

When using Java, you must specify your dependency on the Cloud Dataflow Runner in your `pom.xml`.


```xml
<dependency>
  <groupId>org.apache.beam</groupId>
  <artifactId>beam-runners-spark-3</artifactId>
  <version>2.42.0</version>
</dependency>
```
Si `shading`-ul aplicatiei `jar` folosind `maven shade plugin`:
```xml
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<configuration>
<createDependencyReducedPom>false</createDependencyReducedPom>
<filters>
<filter>
<artifact>*:*</artifact>
<excludes>
<exclude>META-INF/*.SF</exclude>
<exclude>META-INF/*.DSA</exclude>
<exclude>META-INF/*.RSA</exclude>
</excludes>
</filter>
</filters>
</configuration>
<executions>
<execution>
<phase>package</phase>
<goals>
<goal>shade</goal>
</goals>
<configuration>
<shadedArtifactAttached>true</shadedArtifactAttached>
<shadedClassifierName>shaded</shadedClassifierName>
<transformers>
<transformer
implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
</transformers>
</configuration>
</execution>
</executions>
</plugin>
```

Consola:

```bash
mvn compile exec:java -Dexec.mainClass=org.apache.beam.examples.WordCount \
-Dexec.args="--runner=SparkRunner --inputFile=pom.xml --output=counts" -Pspark-runner
```

