<table>
  <tr>
	<td valign="top">
<h3>Categories</h3>
    <p>DDL: Data Definition Language </p>
    <p>DQL: Data Query Language</p>
    <p>DML: Data Manipulation Language</p>
    <p>DCL: Data Control Language</p>
    <p>TCL: Transaction Language</p>
<h3>Commands</h3>
<h4>$${\color{blue}DDL}$$</h4><p>CREATE | DROP | ALTER | TRUNCATE | RENAME | COMMENT </p>
  <h4>$${\color{blue}DQL}$$</h4><p>SELECT</p>
  <h4>$${\color{blue}DML}$$</h4><p>INSERT | UPDATE | DELETE | LOCK | CALL | EXPLAIN PLAN</p>
  <h4>$${\color{blue}DCL}$$</h4><p>GRANT | REVOKE</p>
  <h4>$${\color{blue}TCL}$$</h4><p>COMMIT | ROLLBACK | SAVEPOINT | SET TRANSACTION</p>		
<h3>DDL Examples</h3>
	</td>
    <td valign="top">
<h3>Operators</h3>
      <h4>$${\color{blue}Arithmetic}$$</h4>
      		<p>+ - * /</p>
      <h4>$${\color{blue}Bitwise}$$</h4>
      		<p>& | ^</p>
      <h4>$${\color{blue}Comparison}$$</h4>
      		<p>= < > <= >= !< !> <> != </p>
      <h4>$${\color{blue}Compound}$$</h4>
	   	<p>+= -= *= /= %= &= != ^=</p> 
      <h4>$${\color{blue}Logical}$$</h4>
		<p>AND | OR | NOT | ANY | SOME | ALL | BETWEEN | IN | EXISTS | LIKE | IS NULL | UNIQUE |</p>
<h3>Important Keywords</h3>
			<p>WHERE | DISTINCT | LIMIT | ORDER BY | DESC | ASC | AS | FROM | SET | VALUES | CASE | DEFAULT</p>
    </td>
    <td  valign="top">
<h3>Database objects</h3>
          <p>TABLE | VIEW | SYNONYM
     SEQUENCE | INDEX | TRIGGER</p>
	    <h3>Constraints</h3>
	    <p>NOT NULL | UNIQUE | PRIMARY KEY | FOREIGN KEY | CHECK | DEFAULT</p>
	    <h3>Aggregation Functions</h3>
     <p>AVG | COUNT</p>
     <p>MAX | MIN | SUM</p>
	    <h3>Aggregation Keywords</h3>
     <p>GROUP BY | HAVING
    </td>
  </tr>
</table>

# Quick SQL Cheatsheet

A quick reminder of all relevant SQL queries and examples on how to use them. 

This repository is constantly being updated and added to by the community. 
Pull requests are welcome. Enjoy!

# Table of Contents 
1. [ Finding Data Queries. ](#find)
2. [ Data Modification Queries. ](#modify)
3. [ Reporting Queries. ](#report)
4. [ Join Queries. ](#joins)
5. [ View Queries. ](#view)
6. [ Altering Table Queries.](#alter)
7. [ Creating Table Query.](#create)

<a name="find"></a>
# 1. Finding Data Queries

### **SELECT**: used to select data from a database
* `SELECT` * `FROM` table_name;

### **DISTINCT**: filters away duplicate values and returns rows of specified column
* `SELECT DISTINCT` column_name;

### **WHERE**: used to filter records/rows
* `SELECT` column1, column2 `FROM` table_name `WHERE` condition;
* `SELECT` * `FROM` table_name `WHERE` condition1 `AND` condition2;
* `SELECT` * `FROM` table_name `WHERE` condition1 `OR` condition2;
* `SELECT` * `FROM` table_name `WHERE NOT` condition;
* `SELECT` * `FROM` table_name `WHERE` condition1 `AND` (condition2 `OR` condition3);
* `SELECT` * `FROM` table_name `WHERE EXISTS` (`SELECT` column_name `FROM` table_name `WHERE` condition);

### **ORDER BY**: used to sort the result-set in ascending or descending order
* `SELECT` * `FROM` table_name `ORDER BY` column;
* `SELECT` * `FROM` table_name `ORDER BY` column `DESC`;
* `SELECT` * `FROM` table_name `ORDER BY` column1 `ASC`, column2 `DESC`;

### **SELECT TOP**: used to specify the number of records to return from top of table
* `SELECT TOP` number columns_names `FROM` table_name `WHERE` condition;
* `SELECT TOP` percent columns_names `FROM` table_name `WHERE` condition;
* Not all database systems support `SELECT TOP`. The MySQL equivalent is the `LIMIT` clause
* `SELECT` column_names `FROM` table_name `LIMIT` offset, count;

### **LIKE**: operator used in a WHERE clause to search for a specific pattern in a column
* % (percent sign) is a wildcard character that represents zero, one, or multiple characters
* _ (underscore) is a wildcard character that represents a single character
* `SELECT` column_names `FROM` table_name `WHERE` column_name `LIKE` pattern;
* `LIKE` ‘a%’ (find any values that start with “a”)
* `LIKE` ‘%a’ (find any values that end with “a”)
* `LIKE` ‘%or%’ (find any values that have “or” in any position)
* `LIKE` ‘_r%’ (find any values that have “r” in the second position)
* `LIKE` ‘a_%_%’ (find any values that start with “a” and are at least 3 characters in length)
* `LIKE` ‘[a-c]%’ (find any values starting with “a”, “b”, or “c”

### **IN**: operator that allows you to specify multiple values in a WHERE clause
* essentially the IN operator is shorthand for multiple OR conditions
* `SELECT` column_names `FROM` table_name `WHERE` column_name `IN` (value1, value2, …);
* `SELECT` column_names `FROM` table_name `WHERE` column_name `IN` (`SELECT STATEMENT`);

### **BETWEEN**: operator selects values within a given range inclusive
* `SELECT` column_names `FROM` table_name `WHERE` column_name `BETWEEN` value1 `AND` value2;
* `SELECT` * `FROM` Products `WHERE` (column_name `BETWEEN` value1 `AND` value2) `AND NOT` column_name2 `IN` (value3, value4);
* `SELECT` * `FROM` Products `WHERE` column_name `BETWEEN` #01/07/1999# AND #03/12/1999#;

### **NULL**: values in a field with no value
* `SELECT` * `FROM` table_name `WHERE` column_name `IS NULL`;
* `SELECT` * `FROM` table_name `WHERE` column_name `IS NOT NULL`;

### **AS**: aliases are used to assign a temporary name to a table or column
* `SELECT` column_name `AS` alias_name `FROM` table_name;
* `SELECT` column_name `FROM` table_name `AS` alias_name;
* `SELECT` column_name `AS` alias_name1, column_name2 `AS` alias_name2;
* `SELECT` column_name1, column_name2 + ‘, ‘ + column_name3 `AS` alias_name;

### **UNION**: set operator used to combine the result-set of two or more SELECT statements
* Each SELECT statement within UNION must have the same number of columns
* The columns must have similar data types
* The columns in each SELECT statement must also be in the same order
* `SELECT` columns_names `FROM` table1 `UNION SELECT` column_name `FROM` table2;
* `UNION` operator only selects distinct values, `UNION ALL` will allow duplicates

### **INTERSECT**: set operator which is used to return the records that two SELECT statements have in common
* Generally used the same way as **UNION** above
* `SELECT` columns_names `FROM` table1 `INTERSECT SELECT` column_name `FROM` table2;

### **EXCEPT**: set operator used to return all the records in the first SELECT statement that are not found in the second SELECT statement
* Generally used the same way as **UNION** above
* `SELECT` columns_names `FROM` table1 `EXCEPT SELECT` column_name `FROM` table2;

### **ANY|ALL**: operator used to check subquery conditions used within a WHERE or HAVING clauses
* The `ANY` operator returns true if any subquery values meet the condition
* The `ALL` operator returns true if all subquery values meet the condition
* `SELECT` columns_names `FROM` table1 `WHERE` column_name operator (`ANY`|`ALL`) (`SELECT` column_name `FROM` table_name `WHERE` condition);

### **GROUP BY**: statement often used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns
* `SELECT` column_name1, COUNT(column_name2) `FROM` table_name `WHERE` condition `GROUP BY` column_name1 `ORDER BY` COUNT(column_name2) DESC;

### **HAVING**: this clause was added to SQL because the WHERE keyword could not be used with aggregate functions
* `SELECT` `COUNT`(column_name1), column_name2 `FROM` table `GROUP BY` column_name2 `HAVING` `COUNT(`column_name1`)` > 5;

### **WITH**: often used for retrieving hierarchical data or re-using temp result set several times in a query. Also referred to as "Common Table Expression"
* `WITH RECURSIVE` cte `AS` (<br/>
    &nbsp;&nbsp;`SELECT` c0.* `FROM` categories `AS` c0 `WHERE` id = 1 `# Starting point`<br/>
    &nbsp;&nbsp;`UNION ALL`<br/>
    &nbsp;&nbsp;`SELECT` c1.* `FROM` categories `AS` c1 `JOIN` cte `ON` c1.parent_category_id = cte.id<br/>
  )<br/>
  `SELECT` *<br/>
  `FROM` cte


<a name="modify"></a>
# 2. Data Modification Queries

### **INSERT INTO**: used to insert new records/rows in a table
* `INSERT INTO` table_name (column1, column2) `VALUES` (value1, value2);
* `INSERT INTO` table_name `VALUES` (value1, value2 …);

### **UPDATE**: used to modify the existing records in a table
* `UPDATE` table_name `SET` column1 = value1, column2 = value2 `WHERE` condition;
* `UPDATE` table_name `SET` column_name = value;

### **DELETE**: used to delete existing records/rows in a table
* `DELETE FROM` table_name `WHERE` condition;
* `DELETE` * `FROM` table_name;

<a name="report"></a>
# 3. Reporting Queries

### **COUNT**: returns the # of occurrences
* `SELECT COUNT (DISTINCT` column_name`)`;

### **MIN() and MAX()**: returns the smallest/largest value of the selected column
* `SELECT MIN (`column_names`) FROM` table_name `WHERE` condition;
* `SELECT MAX (`column_names`) FROM` table_name `WHERE` condition;

### **AVG()**: returns the average value of a numeric column
* `SELECT AVG (`column_name`) FROM` table_name `WHERE` condition;

### **SUM()**: returns the total sum of a numeric column
* `SELECT SUM (`column_name`) FROM` table_name `WHERE` condition;

<a name="joins"></a>
# 4. Join Queries

###  **INNER JOIN**: returns records that have matching value in both tables
* `SELECT` column_names `FROM` table1 `INNER JOIN` table2 `ON` table1.column_name=table2.column_name;
* `SELECT` table1.column_name1, table2.column_name2, table3.column_name3 `FROM` ((table1 `INNER JOIN` table2 `ON` relationship) `INNER JOIN` table3 `ON` relationship);

### **LEFT (OUTER) JOIN**: returns all records from the left table (table1), and the matched records from the right table (table2)
* `SELECT` column_names `FROM` table1 `LEFT JOIN` table2 `ON` table1.column_name=table2.column_name;

### **RIGHT (OUTER) JOIN**: returns all records from the right table (table2), and the matched records from the left table (table1)
* `SELECT` column_names `FROM` table1 `RIGHT JOIN` table2 `ON` table1.column_name=table2.column_name;

### **FULL (OUTER) JOIN**: returns all records when there is a match in either left or right table
* `SELECT` column_names `FROM` table1 ``FULL OUTER JOIN`` table2 `ON` table1.column_name=table2.column_name;

### **Self JOIN**: a regular join, but the table is joined with itself
* `SELECT` column_names `FROM` table1 T1, table1 T2 `WHERE` condition;

<a name="view"></a>
# 5. View Queries

### **CREATE**: create a view
* `CREATE VIEW` view_name `AS SELECT` column1, column2 `FROM` table_name `WHERE` condition;

### **SELECT**: retrieve a view
* `SELECT` * `FROM` view_name;

### **DROP**: drop a view
* `DROP VIEW` view_name;

<a name="alter"></a>
# 6. Altering Table Queries

### **ADD**: add a column
* `ALTER TABLE` table_name `ADD` column_name column_definition;

### **MODIFY**: change data type of column
* `ALTER TABLE` table_name `MODIFY` column_name column_type;

### **DROP**: delete a column
* `ALTER TABLE` table_name `DROP COLUMN` column_name;

<a name="create"></a>
# 7. Creating Table Query

### **CREATE**: create a table
* `CREATE TABLE` table_name `(` <br />
   `column1` `datatype`, <br />
   `column2` `datatype`, <br />
   `column3` `datatype`, <br />
   `column4` `datatype`, <br />
   `);`

# SQL languages

**DDL** is short name of Data Definition Language, which deals with database schemas and descriptions, of how the data should reside in the database.

**DCL** is short name of Data Control Language which includes commands such as GRANT, and mostly concerned with rights, permissions and other controls of the database system.

**DML** is short name of Data Manipulation Language which deals with data manipulation, and includes most common SQL statements such INSERT, UPDATE, DELETE etc, and it is used to store, modify, delete and update data in database.

**DQL** is short name of Data Query Language which used for performing queries on the data within schema objects. The purpose of the DQL Command is to get some schema relation based on the query passed to it. SELECT statement is used to retrieve data from the database.

# Datatypes

#### Text types

| Data type        | Description                                                                                                                                                                                                                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CHAR(size)       | Holds a fixed length string (can contain letters, numbers, and special characters). The fixed size is specified in parenthesis. Can store up to 255 characters                                                                                                                                   |
| VARCHAR(size)    | Holds a variable length string (can contain letters, numbers, and special characters). The maximum size is specified in parenthesis. Can store up to 255 characters. Note: If you put a greater value than 255 it will be converted to a TEXT type                                               |
| TINYTEXT         | Holds a string with a maximum length of 255 characters                                                                                                                                                                                                                                           |
| TEXT             | Holds a string with a maximum length of 65,535 characters                                                                                                                                                                                                                                        |
| BLOB             | For BLOBs (Binary Large OBjects). Holds up to 65,535 bytes of data                                                                                                                                                                                                                               |
| MEDIUMTEXT       | Holds a string with a maximum length of 16,777,215 characters                                                                                                                                                                                                                                    |
| MEDIUMBLOB       | For BLOBs (Binary Large OBjects). Holds up to 16,777,215 bytes of data                                                                                                                                                                                                                           |
| LONGTEXT         | Holds a string with a maximum length of 4,294,967,295 characters                                                                                                                                                                                                                                 |
| LONGBLOB         | For BLOBs (Binary Large OBjects). Holds up to 4,294,967,295 bytes of data                                                                                                                                                                                                                        |
| ENUM(x,y,z,etc.) | Let you enter a list of possible values. You can list up to 65535 values in an ENUM list. If a value is inserted that is not in the list, a blank value will be inserted.Note: The values are sorted in the order you enter them.You enter the possible values in this format: ENUM('X','Y','Z') |
| SET              | Similar to ENUM except that SET may contain up to 64 list items and can store more than one choice                                                                                                                                                                                               |

#### Number types

| Data type       | Description                                                                                                                                                                                                                           |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TINYINT(size)   | -128 to 127 normal. 0 to 255 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                                                                  |
| SMALLINT(size)  | -32768 to 32767 normal. 0 to 65535 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                                                            |
| MEDIUMINT(size) | -8388608 to 8388607 normal. 0 to 16777215 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                                                     |
| INT(size)       | -2147483648 to 2147483647 normal. 0 to 4294967295 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                                             |
| BIGINT(size)    | -9223372036854775808 to 9223372036854775807 normal. 0 to 18446744073709551615 UNSIGNED*. The maximum number of digits may be specified in parenthesis                                                                                 |
| FLOAT(size,d)   | A small number with a floating decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter                     |
| DOUBLE(size,d)  | A large number with a floating decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter                     |
| DECIMAL(size,d) | A DOUBLE stored as a string , allowing for a fixed decimal point. The maximum number of digits may be specified in the size parameter. The maximum number of digits to the right of the decimal point is specified in the d parameter |

#### Date types

| Data type   | Description                                                                                                                                                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DATE()      | A date. Format: YYYY-MM-DDNote: The supported range is from '1000-01-01' to '9999-12-31'                                                                                                                                                 |
| DATETIME()  | *A date and time combination. Format: YYYY-MM-DD HH:MI:SSNote: The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'                                                                                                |
| TIMESTAMP() | *A timestamp. TIMESTAMP values are stored as the number of seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD HH:MI:SSNote: The supported range is from '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC |
| TIME()      | A time. Format: HH:MI:SSNote: The supported range is from '-838:59:59' to '838:59:59'                                                                                                                                                    |
| YEAR()      | A year in two-digit or four-digit format.Note: Values allowed in four-digit format: 1901 to 2155. Values allowed in two-digit format: 70 to 69, representing years from 1970 to 2069                                                     |
#### Arithmetic Operators

|Operator|Description
|--------|---------|
| +      | Add
| -      | Subtract
| *      | Multiply
| /      | Divide
| %      | Modulo
#### Bitwise Operator
|Operator|Description
|--------|---------|
| &      | Bitwise AND
| \|      | Bitwise OR
| ^      | Bitwise exclusive OR
#### Comparison Operators
|Operator|Description|
|--------|---------|
|=    | Equal to|
|\>   | Greater than|
|<    | Less than|
|= | Greater than or equal to |
|<= | Less than or equal to |
|<> | Not equal to |
|LIKE ‘%expression%’ | Contains ‘expression’ |
|IN (‘exp1’, ‘exp2’, ‘exp3’) | Contains any of ‘exp1’, ‘exp2’, or ‘exp3’ |

#### Wildcard Characters
In SQL, Wildcards are special characters used with the LIKE and NOT LIKE keywords which allow
us to search data with sophisticated patterns much more efficiently

| Name   | Description                                                                                                                                                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| %      | Equates to zero or more characters. Example 1: Find all users with surnames ending in ‘son’. ```SELECT * FROM users WHERE surname LIKE '%son';``` Example 2: Find all users living in cities containing the pattern ‘che’ ```SELECT * FROM users WHERE city LIKE '%che%';``` |
| _      | Equates to any single character. Example: Find all users living in cities beginning with any 3 characters, followed by ‘chester’. ```SELECT * FROM users WHERE city LIKE '___chester';```|
| [charlist]      | Equates to any single character in the list. Example 1: Find all users with first names beginning with J, H or M. ```SELECT * FROM users WHERE first_name LIKE '[jhm]%';``` Example 2: Find all users with first names beginning letters between A–L. ```SELECT * FROM users WHERE first_name LIKE '[a-l]%';``` Example 3: Find all users with first names not ending with letters between n–s. ```SELECT * FROM users WHERE first_name LIKE '%[!n-s]';```|

#### Complete Set In SQL

| Relational Algebra | SQL                                                          |
| --------- | ----------------------- |
| **Π𝑠(R)** | ```SELECT DISTINCT s FROM R;```	|
| **𝜎𝗉(R)** | ```SELECT * FROM R WHERE p;``` |
| **R×S** | ```SELECT * FROM R,S;``` |
| **R-S** | ```SELECT column(s) FROM R WHERE NOT EXISTS (SELECT column(s) FROM S);``` We can also use ```EXCEPT``` to achieve set difference. |
| **R∪S** | ```SELECT column(s) FROM R UNION SELECT column(s) FROM S;``` |



# DDL & DCL

#### Create
```sql
CREATE DATABASE dbname;
```
#### Drop
```sql
DROP DATABASE dbname;
```

#### Working On A DataBase

List Available Databases:

```sql
SHOW DATABASES;
```
You can run this to select/switch the current database to ```testDB```:

```sql
USE testDB;
```

#### Table

In the below example, data passed to the id column must be an int, whilst the first_name column
has a VARCHAR data type with a maximum of 255 characters.

```sql
CREATE TABLE users (
	id int,
	first_name varchar(255)
);
```

Check if not exist and create

```sql
IF object_id('tbl_customer', n'U') IS NOT NULL DROP TABLE tbl_customer;
GO 
CREATE TABLE tbl_customer ( id_customer INT NOT NULL PRIMARY key, fi_moral_nr INT, name VARCHAR(25) NOT NULL, vorname VARCHAR NOT NULL, wohnort VARCHAR );
GO
```

#### Alter Table
Adds, deletes or edits columns in a table. It can also be used to add and
delete constraints in a table, as per the above.
Example: Adds a new boolean column called ‘approved’ to a table named
‘deals’.

```sql
ALTER TABLE deals
ADD approved boolean;
```
Example 2: Deletes the ‘approved’ column from the ‘deals’ table
```sql
ALTER TABLE deals
DROP COLUMN approved;
```
#### Primary Key
Alter an existing table and set the primary key to the first_name column.
```sql
ALTER TABLE stud
ADD PRIMARY KEY (first_name);
```

#### Alter Column
Changes the data type of a table’s column.
Example: In the ‘users’ table, make the column ‘incept_date’ into a
‘datetime’ type.

```sql
ALTER TABLE users
ALTER COLUMN incept_date datetime;
```

#### Drop Column
Deletes a column from a table.
Example: Removes the first_name column from the users table.

```sql
ALTER TABLE users
DROP COLUMN first_name
```

#### Foreign Key

A foreign key can be applied to one column or many and is used to link 2 tables together in a relational database. As seen in the diagram below, the table containing the foreign key is called the child key, whilst the table which contains the referenced key, or candidate key, is called the parent table. This essentially means that the column data is shared between 2 tables, as a foreign key also prevents invalid data from being inserted which isn’t also present in the parent table.

##### On Updare or On Delete:

It is optional. It specifies what to do with the child data when the parent data is updated or deleted. You have the options of RESTRICT (default), NO ACTION, CASCADE, SET NULL, or SET DEFAULT.

###### ON DELETE|UPDATE CASCADE

It specifies that the child data is deleted when the parent data is deleted. This is dangerous but can be used to make automatic cleanups on secondary tables.

###### ON DELETE|UPDATE NO ACTION

It is used in conjunction with ON DELETE or ON UPDATE. It means that no action is performed with the child data when the parent data is deleted or updated.

###### ON DELETE|UPDATE SET NULL

It is used in conjunction with ON DELETE or ON UPDATE. It means that the child data is set to NULL when the parent data is deleted or updated.

###### ON DELETE|UPDATE SET DEFAULT

It is used in conjunction with ON DELETE or ON UPDATE. It means that the child data is set to their default values when the parent data is deleted or updated.

```sql
ALTER TABLE orders
     ADD FOREIGN KEY (user_id) REFERENCES users(id)
          ON UPDATE CASCADE
          ON DELETE SET NULL;
```
![tbl](https://user-images.githubusercontent.com/30802876/152129948-6f570a63-5e0b-4e1d-ad20-48988c41f5ff.gif)

###### Example 1
Create a new table and turn any columns that reference IDs in other tables into foreign keys.
```sql
CREATE TABLE orders (
id int NOT NULL,
user_id int,
product_id int,
PRIMARY KEY (id),
FOREIGN KEY (user_id) REFERENCES users(id),
FOREIGN KEY (product_id) REFERENCES products(id)
);
```
###### Example 2
Alter an existing table and create a foreign key.
```sql
ALTER TABLE orders
ADD FOREIGN KEY (user_id) REFERENCES users(id);
```
##### Constraint

It creates a new constraint on an existing table, which is used to specify
rules for any data in the table.
Example: Adds a new PRIMARY KEY constraint named ‘user’ on columns
ID and SURNAME.
```sql
ALTER TABLE users
ADD CONSTRAINT user PRIMARY KEY (ID, SURNAME);
```

#### Unique

This constraint ensures all values in a column are unique.

###### Example 1

Adds a unique constraint to the id column when
creating a new users table.

```sql CREATE TABLE users (
CREATE TABLE users (
	id int NOT NULL, name varchar(255) NOT NULL, UNIQUE (id)
);
```

###### Example 2

Alters an existing column to add a UNIQUE
constraint.

```sql ALTER TABLE users
ADD UNIQUE (id);
```

#### Create Type

Registers a new data type for use in the current database. The user who defines a type becomes its owner.
```sql
CREATE TYPE owntype FROM numeric(9,0)
```

#### Declare Variables

```sql
DECLARE @modification SMALLINT = 180;
DECLARE @new_sum INT;
```

#### Login

change password
```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>' OLD_PASSWORD = '<oldWeakPasswordHere>';
```

#### User
create
```sql
CREATE USER romulus FROM LOGIN romulus
```
drop
```sql
DROP user romulus
```

#### Grant/ Revoke
Available permissions: CREATE DEFAULT, CREATE FUNCTION, CREATE
PROCEDURE, CREATE ROLE, CREATE TABLE, CREATE TYPE, CREATE VIEW,
DELETE, EXECUTE, INSERT, SELECT, UPDATE

Grant rights
```sql
GRANT SELECT, INSERT, DELETE, REFERENCES, UPDATE
	TO alex
```
Revoke
```sql
REVOKE INSERT, DELETE, REFERENCES, UPDATE TO alex
```

#### Role
Create
```sql
CREATE ROLE verkauf
```
Add member
```sql
exec sp_addrolemember 'verkauf', 'anna'
```

#### Grant Role
Grant rights

```sql
GRANT SELECT, UPDATE, INSERT, DELETE ON tbl_customer TO verkauf
```

#### View
To create a view, you can do so like this:
```sql
CREATE VIEW priority_users AS
SELECT * FROM users
WHERE country = ‘United Kingdom’;
```
Then in future, if you need to access the stored result set, you can do so like this:
```sql
SELECT * FROM [priority_users];
```
###### Replacing Views
With the CREATE OR REPLACE command, a view can be updated.
```sql
CREATE OR REPLACE VIEW [priority_users] AS
SELECT * FROM users
WHERE country = ‘United Kingdom’ OR country=’USA’;
```
###### Deleting Views
To delete a view, simply use the DROP VIEW command.
```sql
DROP VIEW priority_users;
```

# DML & DQL
#### Insert
Add new rows to a table.
Example: Adds a new vehicle.

```sql
INSERT INTO cars (make, model, mileage, year)
VALUES ('Audi', 'A3', 30000, 2016);
```

#### Delete
Delete data from a table.

###### Example:

 Removes all users.

```sql
DELETE FROM users
```
```sql
TRUNCATE TABLE users
```
###### Example: 

Removes a user with a user_id of 674.

```sql
DELETE FROM users WHERE user_id = 674;
```
#### Update/Set
This two keywords used to update the existing data.

SET used alongside UPDATE to update existing data in a table.

###### Example 1:

Updates the mileage and serviceDue values for a vehicle with an
id of 45 in the cars table.

```sql
UPDATE cars
SET mileage = 23500, serviceDue = 0
WHERE id = 45;
```
###### Example 2:

Updates the value and quantity values for an order with an id of
642 in the orders table.

```sql
UPDATE orders
SET value = 19.49, quantity = 2
WHERE id = 642;
```

#### Select

Used to select data from a database, which is then returned in a results set.
###### Example 1:
Selects all columns from all users.
```sql
SELECT * FROM users;
```
###### Example 2: 
Selects the first_name and surname columns
from all users.xx
```sql
SELECT first_name, surname FROM users;
```
#### Conditional select
Selects the first_name and surname columns where id is 2 AND has address.
```sql
SELECT first_name, surname FROM users WHERE user_id = 2 AND address IS NOT NULL;
```
#### Distinct
Used to select data from a database, which is then returned in a results set.
###### Example:
Returns all countries from the users table, removing any duplicate
values (which would be highly likely)

```sql
SELECT DISTINCT country from users;
```
#### Limit
To limit the number of rows returned by a select statement, you use the LIMIT and OFFSET clauses.
###### Example:
Returns the first three records from the "Customers" table, both queries are the same:

```sql
SELECT * FROM Customers
WHERE Country='Germany'
LIMIT 0,3;
```
```sql
SELECT * FROM Customers
WHERE Country='Germany'
LIMIT 3 OFFSET 0
```
#### Order
Used to sort the result data in ascending (default) or descending order
through the use of ASC or DESC keywords.
Example: Returns countries in alphabetical order.

```sql
SELECT * FROM countries
ORDER BY name DESC;
```
#### Like

Returns true if the operand value matches a pattern.

###### Example 1:

Returns true if the user’s first_name ends with ‘son’.

```sql
SELECT * FROM users
WHERE first_name LIKE '%son';
```

###### Example 2:

Returns true if the user’s first_name with ‘son’.

```sql
SELECT * FROM users
WHERE first_name LIKE '%son%';
```

###### Example 3:

Returns true if the user’s first_name starts with ‘A’ or  ‘B’ or  ‘C’ and length of 4.

```sql
SELECT * FROM users
WHERE first_name LIKE '[^A-C]___';
```

#### Not

Returns true if a record DOESN’T meet the condition.

###### Example:

Returns true if the user’s first_name doesn’t end with ‘son’.

```sql
SELECT * FROM users
WHERE first_name NOT LIKE '%son';
```

#### Case
Change query output depending on conditions.
###### Example: 
Returns users and their subscriptions, along with a new column
called activity_levels that makes a judgement based on the number of
subscriptions.

```sql
SELECT first_name, surname, subscriptions
CASE WHEN subscriptions > 10 THEN 'Very active'
WHEN Quantity BETWEEN 3 AND 10 THEN 'Active'
ELSE 'Inactive'
END AS activity_levels
FROM users;
```

#### And

Used to join separate conditions within a WHERE clause.
Example: Returns events located in London, United Kingdom
```sql
SELECT * FROM events
WHERE host_country='United Kingdom' AND host_
city='London';
```
#### Or
Used alongside WHERE to include data when either condition is true.
###### Example: 
Returns users that live in either Sheffield or Manchester.
```sql
SELECT * FROM users
WHERE city = 'Sheffield' OR 'Manchester';
```
#### As

Renames a table or column with an alias value which only exists for the
duration of the query.
Example: Aliases north_east_user_subscriptions column:

```sql 
SELECT north_east_user_subscriptions AS ne_subs
FROM users
WHERE ne_subs > 5;
```
```sql 
SELECT north_east_user_subscriptions ne_subs
FROM users
WHERE ne_subs > 5;
```
#### Between
Selects values within the given range.
###### Example 1:
Selects stock with a quantity between 100 and 150.
```sql
SELECT * FROM stock
WHERE quantity BETWEEN 100 AND 150;
```
###### Example 2: 
Selects stock with a quantity NOT between 100 and 150.
Alternatively, using the NOT keyword here reverses the logic and selects
values outside the given range.
```sql
SELECT * FROM stock
WHERE quantity NOT BETWEEN 100 AND 150;
```
###### Consider tables

CYCLING
|  id  | name | country |
| :--: | :--: | :-----: |
|  1   |  YK  |   DE    |
|  2   |  ZG  |   DE    |
|  3   |  WT  |   PL    |
| ...  | ...  |   ...   |

SKATING
|  id  | name | country |
| :--: | :--: | :-----: |
|  1   |  YK  |   DE    |
|  2   |  DF  |   DE    |
|  3   |  AK  |   PL    |
| ...  | ...  |   ...   |


#### Union

Combines the results from 2 or more SELECT statements and returns only
distinct values.
###### Example:
This query displays German cyclists together with German skaters:

```sql
SELECT name FROM cycling WHERE country = 'DE'
UNION
SELECT name FROM skating WHERE country = 'DE';
```
```UNION ALL``` The same as UNION, but includes duplicate values.

#### Intersect
INTERSECT returns only rows that appear in both result sets.
###### Example:
This query displays German cyclists who are also German skaters at the same time:
```sql
SELECT name FROM cycling WHERE country = 'DE'
INTERSECT
SELECT name FROM skating WHERE country = 'DE';
```
```INTERSECT ALL``` The same as INTERSECT, but includes duplicate values.

#### Except
EXCEPT returns only the rows that appear in the first result set but do not appear
in the second result set.
###### Example:
This query displays German cyclists unless they are also German skaters at the
same time:
```sql
SELECT name FROM cycling WHERE country = 'DE'
EXCEPT
SELECT name FROM skating WHERE country = 'DE';
```
```MINUS``` is the same as ```EXCEPT```.
```EXCEPT ALL``` The same as EXCEPT, but includes duplicate values.

###### Consider tables:
COUNTRY
|  id  |  name   | population |  area  |
| :--: | :-----: | :--------: | :----: |
|  1   | France  |  66600000  | 640680 |
|  2   | Germany |  80700000  | 357000 |
| ...  |   ...   |    ...     |  ...   |

CITY
|  id  |  name  | country_id | population | rating |
| :--: | :----: | :--------: | :--------: | :----: |
|  1   | Paris  |     1      |  2243000   |   5    |
|  2   | Berlin |     2      |  3460000   |   3    |
| ...  |  ...   |    ...     |    ...     |  ...   |



#### Common Functions

```AVG()``` - Returns the average value.

```sql
SELECT city_id, AVG(rating)
FROM ratings
GROUP BY city_id;
```

```COUNT(*)``` - Returns the number of rows.

Find out the number of cities with non-null ratings:

```sql
SELECT COUNT(rating)
FROM city;
```

```MAX()``` - Returns the largest value.
```MIN()``` - Returns the smallest value.
Find out the smallest and the greatest country populations:

```sql
SELECT MIN(population), MAX(population)
FROM country;
```

```SUM()``` - Returns the sum.
Find out the total population of cities in respective countries:

```sql
SELECT country_id, SUM(population)
FROM city
GROUP BY country_id;
```

```FIRST()``` - Returns the first value.
```LAST()``` - Returns the last value.

Find out the name of first customer in Customers table:

```sql
SELECT FIRST(CustomerName) AS FirstCustomer 
FROM Customers;
```



------



# Sub Queries

A subquery is a query that is nested inside another query, or inside another subquery.
There are different types of subqueries.

## - Single value

The simplest subquery returns exactly one column and exactly one row. It can be
used with comparison operators =, <, <=, >, or >=.
This query finds cities with the same rating as Paris:

```sql
SELECT name FROM city
WHERE rating = (
	SELECT rating
	FROM city
	WHERE name = 'Paris'
);
```

## - Multiple value

A subquery can also return multiple columns or multiple rows. Such subqueries can be
used with operators IN, EXISTS, ALL, or ANY.
This query finds cities in countries that have a population above 20M:

```sql
SELECT name
FROM city
WHERE country_id IN (
	SELECT country_id
	FROM country
	WHERE population > 20000000
);
```

#### In

Used alongside a WHERE clause as a shorthand for multiple OR conditions.
So instead of:

```sql
SELECT * FROM users
WHERE country = 'USA' OR country = 'United Kingdom' OR
country = 'Russia' OR country = 'Australia';
```

You can use:

```sql
SELECT * FROM users
WHERE country IN ('USA', 'United Kingdom', 'Russia',
'Australia');
```

```NOT IN``` works exactly the opposite of ```IN ```.

#### Any

Returns true if any of the subquery values meet the given condition.
Example: Returns products from the products table which have received
orders – stored in the orders table – with a quantity of more than 5.
The main difference between the ```ANY``` and ```IN``` keywords in SQL is that ```ANY``` allows for more flexible comparison operators, whereas ```IN``` only checks for equality.

```sql
SELECT name
FROM products
WHERE productId = ANY (SELECT productId FROM orders WHERE
quantity > 5);
```

```SOME``` is the same as ```ANY```.

#### All

Returns true if all of the subquery values meet the passed condition.
Example: Returns the users with a higher number of tasks than the user
with the highest number of tasks in the HR department (id 2)

```sql
SELECT first_name, surname, tasks_no
FROM users
WHERE tasks_no > ALL (SELECT tasks FROM user WHERE
department_id = 2);
```

## - Correlated

A correlated subquery refers to the tables introduced in the outer query. A correlated
subquery depends on the outer query. It cannot be run independently from the outer
query.
This query finds cities with a population greater than the average population in the
country:

```sql
SELECT *
FROM city main_city
WHERE population > (
	SELECT AVG(population)
	FROM city average_city
	WHERE average_city.country_id = main_city.country_id
);
```

This query finds countries that have at least one city:

```sql
SELECT name
FROM country
WHERE EXISTS (
	SELECT *
	FROM city
	WHERE country_id = country.id
);
```

#### Exists

Checks for the existence of any record within the subquery, returning true if
one or more records are returned.

###### Example: 

Lists any dealerships with a deal finance percentage less than 10.

```sql
SELECT dealership_name
	FROM dealerships WHERE 
		EXISTS (SELECT deal_name FROM deals WHERE
			dealership_id = deals.dealership_id AND finance_percentage < 10);
```

```NOT EXISTS```  works exactly the opposite of ```EXISTS```.

###### Example: 

This query finds supplier numbers who supplied a part with quantity of at least 50:

```sql
SELECT spone.s# FROM sp spone 
		WHERE NOT EXISTS (SELECT sptwo.s# FROM sp sptwo 
				WHERE spone.qty < 50);
```



------



#### Group By

Used alongside aggregate functions (COUNT, MAX, MIN, SUM, AVG)
to group the results.

###### Example: 
Find out the total population of cities in respective countries:
```sql
SELECT country_id, SUM(population)
FROM city
GROUP BY country_id;
```
#### Having

It’s used in the place of WHERE with aggregate functions.

###### Example: 

Find out the average rating for cities in respective countries if the average is above 3.0:

```sql SELECT COUNT(user_id), active_orders
SELECT country_id, AVG(rating)
 FROM city
	GROUP BY country_id
		HAVING AVG(rating) > 3.0;
```

#### With

WITH clause allows you to give a sub-query block a name (a process also called sub-query refactoring), which can be referenced in several places within the main SQL query. 

###### Example 1:

 Find all the cities that rating is more than the average rating of all cities. 

```sql
WITH temporaryTable(averageValue) 
	AS (SELECT AVG(rating) FROM city)
        SELECT id,name, rating FROM city, temporaryTable 
        	WHERE city.rating > temporaryTable.averageValue;
```

# Join

There are a number of different joins available for you to use:
* Inner Join (Default): Returns any records which have matching values in both tables.
* Left Join: Returns all of the records from the first table, along with any matching records from
  the second table.
* Right Join: Returns all of the records from the second table, along with any matching records
  from the first.
* Full Join: Returns all records from both tables when there is a match.
  A common way of visualising how joins work is like this:

![sql join summary](https://user-images.githubusercontent.com/30802876/152129944-82f37edd-068c-46fe-8374-1d2abeaf1b08.gif)

#### Inner Join

JOIN (or explicitly INNER JOIN) returns rows that have
matching values in both tables.

```sql
SELECT city.name, country.name
FROM city
[INNER] JOIN country
 ON city.country_id = country.id;
```



#### Full Join

FULL JOIN (or explicitly FULL OUTER JOIN) returns all rows from both tables – if there's no matching row in the second table, NULLs are returned.

```sql
SELECT city.name, country.name
FROM city
FULL [OUTER] JOIN country
 ON city.country_id = country.id;
```



#### Left Join

LEFT JOIN returns all rows from the left table with corresponding rows from the right table. If there's no matching row, NULLs are returned as values from the second table.

```sql
SELECT city.name, country.name
FROM city
LEFT JOIN country
 ON city.country_id = country.id;
```



#### Right Join

RIGHT JOIN returns all rows from the right table with corresponding rows from the left table. If there's no matching row, NULLs are returned as values from the left table.

```sql
SELECT city.name, country.name
FROM city
RIGHT JOIN country
 ON city.country_id = country.id;
```



#### Cross Join

CROSS JOIN returns all possible combinations of rows from both tables. There are two syntaxes available.

```sql
SELECT city.name, country.name
FROM city
CROSS JOIN country;
```

```sql
SELECT city.name, country.name
FROM city, country;
```



#### Natural Join

NATURAL JOIN will join tables by all columns with the same name.

```sql
SELECT city.name, country.name
FROM city
NATURAL JOIN country;
```

NATURAL JOIN is very rarely used in practice.



# Transactions

Run a transaction
```sql
START TRANSACTION;
SELECT @A:=SUM(salary) FROM table1 WHERE type=1;
UPDATE table2 SET summary=@A WHERE type=1;
COMMIT;
-- or rollback
```

# Relational division

The database scheme consists of three tables:

**S ([S#](#), sname, city)**
**SP ([S#](#), [P#](#), qty)**
**P ([P#](#), pname, color)**

![tables](https://user-images.githubusercontent.com/30802876/274906644-e796a700-7d46-4fed-b6b2-78118fa48e5c.gif)

Let`s consider task:

```
Determine number of suppliers who have supplied all parts.
```
The keyword here is “all” which means that supplier numbers in **SP** table must have all part numbers (**P#**).

There is special operation for solving this type of tasks in the relational algebra. This operation is relational division (÷).

This operation makes solution of considering task very simple [1]:
```
SP[S#] ÷ P[S#]
```
The relational division operation is superfluous. It can be expressed by the complete set of the relational algebra. Perhaps, that`s the reason why it absents in the SQL.

This is division in relational algebra:	


$$
R ÷ S = Π_{R-S} (R) - Π_{R-S} ((Π_{R-S} (R) × S) - R)
$$


Let`s introduce three methods of implementation of relational division in SQL on considering example.

### Grouping

If suppose that there is only three types of part in table **P**, we may group data by supplier number and count quantity of their parts. Then we select only suppliers with quantity equal three.
like this,

```sql
SELECT `s#` 
FROM sp 
	GROUP BY `s#`
	HAVING COUNT(`p#`) = (SELECT COUNT(`p#`) FROM p);
```

------

### Subtraction

```sql
SELECT DISTINCT `s#` 
FROM s 
WHERE NOT EXISTS (
    SELECT `p#` FROM p
    EXCEPT
    SELECT `p#` FROM sp WHERE s.`s#` = sp.`s#`);
```
This query may be rewritten in shorter form if we take into account fact that the ALL predicate returns TRUE if the subquery have no rows:
```sql
SELECT DISTINCT `s#` 
FROM s 
WHERE `s#` = ALL ( 
    SELECT `p#` FROM p
    EXCEPT
    SELECT `p#` FROM sp WHERE s.`s#` = sp.`s#`);
```
------

### Existence

```sql
SELECT `s#` 
FROM s
WHERE NOT EXISTS (SELECT `p#` 
		  FROM p
		  WHERE NOT EXISTS (SELECT `p#` 
                                    FROM sp
				    WHERE s.`s#`= sp.`s#` AND p.`p#` = sp.`p#`));
```
All solutions, except first one, are using correlation subquery.

