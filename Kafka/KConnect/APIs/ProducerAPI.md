# Producer API in Kafka


Producer API-ul permite aplicațiilor să trimită fluxuri de date către subiecte din clusterul Kafka.
Exemple care arată cum se utilizează producătorul sunt date în javadocs.

Pentru a utiliza producătorul, puteți utiliza următoarea dependență Maven:

```xml
<dependency>
	<groupId>org.apache.kafka</groupId>
	<artifactId>kafka-clients</artifactId>
	<version>3.6.1</version>
</dependency>
```
Când utilizați Scala, puteți include opțional biblioteca `kafka-streams-scala`. Documentația suplimentară despre utilizarea `Kafka Streams DSL` pentru Scala este disponibilă în ghidul dezvoltatorului.

Pentru a utiliza `Kafka Streams DSL` pentru Scala pentru Scala 2.13, puteți utiliza următoarea dependență Maven:


```xml
<dependency>
	<groupId>org.apache.kafka</groupId>
	<artifactId>kafka-streams-scala_2.13</artifactId>
	<version>3.6.1</version>
</dependency>
```


