# SQL

## Ce este SQL?

- SQL este un limbaj standard pentru stocarea, manipularea și preluarea datelor în baze de date.
- SQL înseamnă *Structured Query Language*
- SQL îți permite să accesezi și să manipulezi bazele de date
- SQL a devenit un standard al *American National Standards Institute (ANSI)* în 1986 și al *International Organization for Standardization (ISO)* în 1987

## Ce poate face SQL?

- SQL poate executa interogări asupra unei baze de date
- SQL poate recupera date dintr-o bază de date
- SQL poate insera înregistrări într-o bază de date
- SQL poate actualiza înregistrări într-o bază de date
- SQL poate șterge înregistrări dintr-o bază de date
- SQL poate crea baze de date noi
- SQL poate crea tabele noi într-o bază de date
- SQL poate crea proceduri stocate într-o bază de date
- SQL poate crea vederi într-o bază de date
- SQL poate seta permisiuni pentru tabele, proceduri și vederi

## SQL este un standard - DAR...

Cu toate că SQL este un standard ANSI/ISO, există diferite versiuni ale limbajului SQL.

Cu toate acestea, pentru a fi conforme cu standardul ANSI, toate susțin cel puțin comenzile majore (cum ar fi `SELECT`, `UPDATE`, `DELETE`, `INSERT`, `WHERE`) într-un mod similar.

**Notă:** Majoritatea programelor de baze de date SQL au și extensii proprietare proprii, în plus față de standardul SQL!

**Utilizarea SQL în Site-ul Web al Tău**

Pentru a construi un site web care afișează date dintr-o bază de date, vei avea nevoie de:

1. Un program de bază de date RDBMS (de exemplu, MS Access, SQL Server, MySQL)
2. Utilizarea unui limbaj de scripting de server, cum ar fi PHP sau ASP
3. Utilizarea SQL pentru a obține datele dorite
4. Utilizarea HTML / CSS pentru a stiliza pagina


## RDBMS
RDBMS înseamnă Relational Database Management System.

RDBMS stă la baza SQL și a tuturor sistemelor moderne de baze de date, cum ar fi MS SQL Server, IBM DB2, Oracle, MySQL și Microsoft Access.

Datele în RDBMS sunt stocate în obiecte de bază de date numite tabele. O tabelă este o colecție de înregistrări de date legate și constă din coloane și rânduri.

Uitați-vă la tabela "Customers":

```sql
SELECT * FROM Customers;
```

Fiecare tabel este divizat în entități mai mici numite câmpuri. Câmpurile în tabela "`Customers`" constau din `CustomerID`, `CustomerName`, `ContactName`, `Address`, `City`, `PostalCode` și `Country`. Un câmp este o coloană într-un tabel proiectată pentru a menține informații specifice despre fiecare înregistrare în tabel.

O înregistrare, numită și rând, reprezintă fiecare intrare individuală care există într-un tabel. De exemplu, există 91 de înregistrări în tabela "Customers". O înregistrare este o entitate orizontală într-un tabel.

O coloană este o entitate verticală într-un tabel care conține toate informațiile asociate cu un câmp specific într-un tabel.
