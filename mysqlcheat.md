### MySQL Queries ###

#### User Administration ####

Syntax:
```
CREATE USER '<username>'@'<ip address>' IDENTiFIED BY '<password>'
```

Example:
```sql
CREATE USER 'root'@'192.168.1.10' IDENTIFIED BY 'mysecretpass'
```

Give all access:
```sql
GRANT ALL PRIVILEGES ON *.* TO '<username>'@'<ip>' IDENNTIFIED BY '<password>'
``` 

Give access to specific DB:
```sql
GRANT ALL PRIVILEGES ON <dbname>.* TO '<username>'@'<ip>' IDENTIFIED BY '<password>'
```

#### Database Queries #####

To show all the databases:
```sql
SHOW DATABASES;
```

Creating a database:
```sql
CREATE DATABASE database_name;
```

Delete database:
```sql
DROP DATABASE db_name;
```

Selecting the database:
```sql
USE database_name;
```

List all the table in a DB:
```sql
SHOW TABLES;
```

#### Table Queries ####

Show all the information of a table:
```sql
DESCRIBE tb_name;
```

Creating a table:

*Syntax:*
```sql
CREATE TABLE tb_name(column1_name column1_type, column2_name column2_type, ...);
```

*Types:*
* CHAR(size) - Character column | Holds 255 chars.
* VARCHAR(size) - String | Holds 255 chars.
* TEXT - String | Larger than 255.
* INT(size) - 32 bit integer | size in the number of digits.
* UNSIGNED INT - 32 bit unsigned integer.
* FLOAT(size, d) - Floating number | size is the number of digits | d is the number of digits after decimal point.
* DOUBLE(size, d) - Same as FLOAT but 64 bit.
* DATE() - YYYY-MM-DD
* DATETIME() - YYYY-MM-DD HH:MI:SS
* TIMESTAMP - YYYY-MM-DD HH:MI:SS

**Example:**
```sql
CREATE TABLE movies(id INT(11) NOT NULL PRIMARY KEY AUTO_INCREMENT, name VARCHAR(50), rating FLOAT(5), cast VARCHAR(255), story TEXT, TIMESTAMP);
```

Inserting records in a table:
```sql
INSERT INTO tb_name(column1, column2, ...) VALUES(val1, val2, ...);
```

Changing existing record of a table:
```sql
UPDATE tb_name SET column1 = value1, column2 = value2 WHERE condition;
```

Count number of rows/records in a table:
```sql
SELECT COUNT(*) FROM table_name;
```

Delete records from table:
```sql
DELETE FROM tb_name WHERE condition;
DELETE FROM tb_name;	--Will delete all records
```

Altering the table data(adding new column, deleting column, changing data type of a column):
```sql
ALTER TABLE tb_name ADD column_name data_type;
ALTER TABLE tb_name DROP column_name;
ALTER TABLE tb_name MODIFY column_name new_data_tyep;
```

Delete all the table data but not the table:
```sql
TRUNCATE TABLE tb_name;
```

Delete table:
```sql
DROP TABLE tb_name;
```

#### Fetching Data From a Table ####

Selecting records from table:
```sql
SELECT column1, column2, ... FROM tb_name;
SELECT * FROM tb_name;
SELECT DISTINCT column1, column2, ... FROM tb_name; --Will return only uniqe values
SELECT * FROM tb_name WHERE condition;
SELECT CAST(float_column as DECIMAL(30, 16)) FROM tb_name;
```
