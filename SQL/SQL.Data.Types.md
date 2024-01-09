# Tipurile de date SQL

Fiecare coloană dintr-un tabel al bazei de date trebuie să aibă un nume și un tip de date.

Un dezvoltator SQL trebuie să decidă ce tip de date vor fi stocate în fiecare coloană atunci când creează un tabel. Tipul de date este un ghid pentru SQL pentru a înțelege ce tip de date este așteptat în interiorul fiecărei coloane și, de asemenea, identifică modul în care SQL va interacționa cu datele stocate.

Iată o listă cu tipurile de date din MySQL 8.0, SQL Server și MS Access, traduse și formatate într-un tabel Markdown:

### MySQL Data Types (Version 8.0)

#### String Data Types

| Data Type      | Description                                               | Max Size                | Storage            |
| -------------- | --------------------------------------------------------- | ----------------------- | ------------------ |
| CHAR(size)      | A FIXED length string                                     | 255 characters          | Defined width      |
| VARCHAR(size)   | A VARIABLE length string                                  | 65535 characters        | 2 bytes + chars    |
| BINARY(size)    | Equal to CHAR(), stores binary byte strings              |                         | 1 byte             |
| VARBINARY(size) | Equal to VARCHAR(), stores binary byte strings           | 65535 bytes             | 2 bytes + chars    |
| TINYBLOB        | For BLOBs, max length: 255 bytes                          |                         | 1 byte             |
| TINYTEXT        | Holds a string, max length: 255 characters               | 255 characters         | 1 byte + chars     |
| TEXT(size)      | Holds a string, max length: 65535 bytes                   | 65535 bytes             | 2 bytes + chars    |
| BLOB(size)      | For BLOBs, max length: 65535 bytes                        | 65535 bytes             | 2 bytes + chars    |
| MEDIUMTEXT      | Holds a string, max length: 16777215 characters           | 16777215 characters     | 3 bytes + chars    |
| MEDIUMBLOB      | For BLOBs, max length: 16777215 bytes                     | 16777215 bytes          | 3 bytes + chars    |
| LONGTEXT        | Holds a string, max length: 4294967295 characters         | 4294967295 characters  | 4 bytes + chars    |
| LONGBLOB        | For BLOBs, max length: 4294967295 bytes                   | 4294967295 bytes       | 4 bytes + chars    |
| ENUM(val1, ...) | A string with a single value from a list                  | Up to 65535 values      | 1 or 2 bytes       |
| SET(val1, ...)  | A string with multiple values from a list                | Up to 64 values         | 1, 2, 3, 4, or 8 bytes |

#### Numeric Data Types

| Data Type       | Description                                               | Storage               |
| --------------- | --------------------------------------------------------- | ---------------------- |
| BIT(size)        | A bit-value type                                          | 1 to 64 bits          |
| TINYINT(size)   | A very small integer, signed range: -128 to 127           | 1 byte                |
| BOOL / BOOLEAN  | Zero is false, nonzero values are true                    | 1 byte                |
| SMALLINT(size)  | A small integer, signed range: -32768 to 32767            | 2 bytes               |
| MEDIUMINT(size) | A medium integer, signed range: -8388608 to 8388607        | 3 bytes               |
| INT(size)       | A medium integer, signed range: -2147483648 to 2147483647 | 4 bytes               |
| INTEGER(size)   | Equivalent to INT(size)                                   | 4 bytes               |
| BIGINT(size)    | A large integer, signed range: -9223372036854775808 to 9223372036854775807 | 8 bytes |
| FLOAT(size, d)  | A floating-point number, deprecated syntax                 | 4 or 8 bytes          |
| FLOAT(p)        | A floating-point number, MySQL uses p to determine FLOAT or DOUBLE | 4 or 8 bytes |
| DOUBLE(size, d) | A normal-size floating-point number                       | 8 bytes               |
| DECIMAL(size, d)| An exact fixed-point number                               | 5-17 bytes            |
| DEC(size, d)    | Equivalent to DECIMAL(size, d)                             | 5-17 bytes            |

#### Date and Time Data Types

| Data Type          | Description                                               | Storage               |
| ------------------ | --------------------------------------------------------- | ---------------------- |
| DATE               | A date, format: YYYY-MM-DD                                | 3 bytes               |
| DATETIME(fsp)     | A date and time combination, format: YYYY-MM-DD hh:mm:ss  | 6-8 bytes             |
| TIMESTAMP(fsp)    | A timestamp, stored as seconds since '1970-01-01 00:00:00' | 4-7 bytes             |
| TIME(fsp)         | A time, format: hh:mm:ss                                  | 3-5 bytes             |
| YEAR              | A year in four-digit format, values allowed: 1901 to 2155  | 1 byte                |

### SQL Server Data Types

#### String Data Types

| Data Type      | Description                                   | Max Size                 | Storage            |
| -------------- | --------------------------------------------- | ------------------------ | ------------------ |
| char(n)        | Fixed width character string                  | 8000 characters          | Defined width      |
| varchar(n)     | Variable width character string               | 8000 characters          | 2 bytes + chars    |
| varchar(max)   | Variable width character string               | 1,073,741,824 characters | 2 bytes + chars    |
| text           | Variable width character string               | 2GB of text data         | 4 bytes + chars    |
| nchar          | Fixed width Unicode string                    | 4000 characters          | Defined width x 2  |
| nvarchar       | Variable width Unicode string                 | 4000 characters          | 2 bytes + chars    |
| nvarchar(max)  | Variable width Unicode string                 | 536,870,912 characters   | 2 bytes + chars    |
| ntext          | Variable width Unicode string                 | 2GB of text data         | 4 bytes + chars    |
| binary(n)      | Fixed width binary string                     | 8000 bytes               | n bytes            |
| varbinary      | Variable width binary string                  | 8000 bytes               | n bytes            |
| varbinary(max) | Variable width binary string                  | 2GB                      | n bytes            |
| image          | Variable width binary string                  | 2GB                      | n bytes            |

Sper că această versiune este mai ușor de citit.

#### Numeric Data Types

| Data Type         | Description                                               | Storage               |
| ----------------- | --------------------------------------------------------- | ---------------------- |
| bit               | Integer that can be 0, 1, or NULL                          | 1 bit                 |
| tinyint           | Whole numbers from 0 to 255                                | 1 byte                |
| smallint          | Whole numbers between -32,768 and 32,767                   | 2 bytes               |
| int               | Whole numbers between -2,147,483,648 and 2,147,483,647    | 4 bytes               |
| bigint            | Whole numbers between -9,223,372,036,854,775,808 and 9,223,372,036,854,775,807 | 8 bytes |
| decimal(p, s)     | Fixed precision and scale numbers                          | 5-17 bytes            |
| numeric(p, s)     | Fixed precision and scale numbers                          | 5-17 bytes            |
| smallmoney        | Monetary data from -214,748.3648 to 214,748.3647           | 4 bytes               |
| money             | Monetary data from -922,337,203,685,477.5808 to 922,337,203,685,477.5807 | 8 bytes |
| float(n)          | Floating precision number data                            | 4 or 8 bytes          |
| real              | Floating precision number data                            | 4 bytes               |

#### Date and Time Data Types

| Data Type         | Description                                               | Storage               |
| ----------------- | --------------------------------------------------------- | ---------------------- |
| datetime          | From January 1, 1753 to December 31, 9999 with an accuracy of 3.33 milliseconds | 8 bytes |
| datetime2         | From January 1, 0001 to December 31, 9999 with an accuracy of 100 nanoseconds | 6-8 bytes |
| smalldatetime     | From January 1, 1900 to June 6, 2079 with an accuracy of 1 minute | 4 bytes |
| date              | Store a date only, from January 1, 0001 to December 31, 9999 | 3 bytes              |
| time              | Store a time only to an accuracy of 100 nanoseconds        | 3-5 bytes             |
| datetimeoffset    | The same as datetime2 with the addition of a time zone offset | 8-10 bytes           |
| timestamp         | Stores a unique number that gets updated every time a row gets created or modified | 8 bytes |
