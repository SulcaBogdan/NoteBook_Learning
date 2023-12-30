# Data in Java

Java nu are o clasă de `Date` încorporată, dar putem importa pachetul `java.time` pentru a lucra cu API-ul de date și timp. Pachetul include multe clase pentru lucrul cu date și timp. De exemplu:

| Clasă              | Descriere                                                   |
| ------------------ | ----------------------------------------------------------- |
| `LocalDate`        | Reprezintă o dată (an, lună, zi (yyyy-MM-dd))               |
| `LocalTime`        | Reprezintă o oră (oră, minut, secundă și nanosecunde (HH-mm-ss-ns)) |
| `LocalDateTime`    | Reprezintă atât o dată, cât și o oră (yyyy-MM-dd-HH-mm-ss-ns) |
| `DateTimeFormatter` | Formatter pentru afișarea și analizarea obiectelor de tip data și timp |



## Printarea data curenta

Pentru a afișa data curentă, importă clasa `java.time.LocalDate` și folosește metoda `now()`:

```java
import java.time.LocalDate; // import the LocalDate class

public class Main {
  public static void main(String[] args) {
    LocalDate myObj = LocalDate.now(); // Create a date object
    System.out.println(myObj); // Display the current date
  }
}

output:
2023-12-30
```

## Printarea timpului curent

Pentru a afișa ora curentă (oră, minut, secundă și nanosecunde), importă clasa `java.time.LocalTime` și folosește metoda `now()`:

```java
import java.time.LocalTime; // import the LocalTime class

public class Main {
  public static void main(String[] args) {
    LocalTime myObj = LocalTime.now();
    System.out.println(myObj);
  }
}

output:
17:56:41.315497
```

## Printarea datei si timpului curent

Pentru a afișa data și ora curentă, importă clasa `java.time.LocalDateTime` și folosește metoda `now()`:

```java
import java.time.LocalDateTime; // import the LocalDateTime class

public class Main {
  public static void main(String[] args) {
    LocalDateTime myObj = LocalDateTime.now();
    System.out.println(myObj);
  }
}

output:
2023-12-30T17:56:41.315579
```

## Formatarea datei si a timpului

Litera "T" în exemplul de mai sus este folosită pentru a separa data de timp. Poți utiliza clasa `DateTimeFormatter` cu metoda `ofPattern()` din același pachet pentru a formata sau analiza obiecte de tip data și timp. Exemplul următor va elimina atât litera "T", cât și nanosecundele din data și ora:

```java
import java.time.LocalDateTime; // Import the LocalDateTime class
import java.time.format.DateTimeFormatter; // Import the DateTimeFormatter class

public class Main {
  public static void main(String[] args) {
    LocalDateTime myDateObj = LocalDateTime.now();
    System.out.println("Before formatting: " + myDateObj);
    DateTimeFormatter myFormatObj = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");

    String formattedDate = myDateObj.format(myFormatObj);
    System.out.println("After formatting: " + formattedDate);
  }
}

output:
Before Formatting: 2023-12-30T17:56:41.315089
After Formatting: 30-12-2023 17:56:41
```

Metoda `ofPattern()` acceptă o varietate de valori, dacă vrei să afișezi data și ora într-un format diferit. De exemplu:

| Valoare        | Exemplu               |
| -------------- | --------------------- |
| `yyyy-MM-dd`   | "1988-09-29"          |
| `dd/MM/yyyy`   | "29/09/1988"          |
| `dd-MMM-yyyy`  | "29-Sep-1988"         |
| `E, MMM dd yyyy`| "Thu, Sep 29 1988"    |








