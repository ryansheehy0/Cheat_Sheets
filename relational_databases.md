[Home](./README.md)

# Relational Databases
Relational databases organize things into tables with each element in the table having a unique id/primary key. Elements in these tables can connect to elements from other tables by having a column of that connection's unique id.

Rows are elements and columns are attributes. Each cell contains one value of a specific data type.

- A **surrogate key** is a unique id that has no mapping to anything in the real world. It is just used internally in the db.
- A **natural key** is a unique attribute that has a real world mapping to something in the real world. Like a unique email address.
- A **foreign key** is an attribute on a table that links to a unique key of another table.
- A **composite key** is a primary key that is made up of 2 attributes. Only both of the attributes can uniquely identify an element.

Table 1

| email(natural key)  | username |
|---------------------|----------|
| user123@example.com | user123  |
| alice@example.com   | alice    |
| bob@example.com     | bob      |

Table 2

| post_id(surrogate key) | email(foreign key)  | message      |
|------------------------|---------------------|--------------|
| 1                      | user123@example.com | Hello World  |
| 2                      | alice@example.com   | My Thoughts  |
| 3                      | user123@example.com | Another Post |

- A **schema** refers to how the database is layed out. The structure or design of the database.
- A **query** is a search in the database in order to read information.
- **Create Read Update Delete(CRUD)** are the 4 main operation when dealing with databases.

## Atomicity Consistency Isolation Durability(ACID)
One of the fundamental guarantees a transaction(Sequence of CRUD operations) must satisfy for a database.

**Atomicity** means that a transaction either executes entirely or not at all. If part of the transaction doesn't work then the database is not changed.

**Consistency** means the database only goes from one valid state to another valid state. The database can never be in a state that breaks its own internal rules. For example, an attribute always containing a consistent data type.

**Isolation** means that 2 transactions happening at the same time do not interfere with one another. No race conditions.

**Durability** means that once a database is changed those changes will persist and not be lost. This may include some form of backups.

## Attribute Properties
Attributes(columns) have various properties that define their behavior/internal rules.

- **Nullable** defines if an attribute contain NULL value or not.
- **Primary Key**, **Unique Key**, or **None**
  - **Primary Key** defines a unique id to each element/row. Used to link elements from one table to another. No NULL values.
  - **Unique Key** enforces uniqueness of each value, but allows NULL values.
- **Index** improves data retrieval speeds. You can query using the index directly. Like the key in a JS object.
- **Auto Increment** allows the column to automatically generate a unique value and is often used for primary keys.
- **Unsigned** used for numerical data types and decides if they can have signed or unsigned values.
- Data types

| Most Common Data Types | Description                                                        |
|------------------------|--------------------------------------------------------------------|
| INT                    | Integers of 4 bytes.                                               |
| BIGINT                 | Integers of 8 bytes.                                               |
| FLOAT                  | Floating-point numbers                                             |
| VARCHAR(#)             | Strings with a pre-defined length, limited to # of characters.     |
| TEXT                   | Strings of undefined length.                                       |
| DATE                   | Date value in 'YYYY-MM-DD' format.                                 |
| TIME                   | Time value in 'HH:MM:SS' format.                                   |
| DATETIME               | Date and time value in 'YYYY-MM-DD HH:MM:SS' format.               |
| BOOLEAN                | Boolean value representing true or false.                          |
| CHAR(#)                | Fixed-length character string. If shorter then padded with spaces. |
| BLOB                   | Binary large object, for storing binary data.                      |

When using TEXT always run a delete or update with a select and where clause. Otherwise, it might mess the whole database.

VARCHAR(255) is often used over TEXT because it takes up less space.

## Structured Query Language(SQL)
SQL is a language used to interact with relational databases. Tends to retrieve data very fast.

- SQL keywords are not case sensitive, however capital letters for the commands are recommended.
- Table names and column names tend to be put in lowercase with underscores instead of spaces.
- Strings are put inside single quotes. 's
- Commands in SQL end in semi-columns. ;s
- `--`s are used for comments in SQL

### Database Commands
```SQL
-- Creating a new database
CREATE DATABASE record_company;

-- This tells SQL which database to use when using commands.
USE record_company;

-- Sees what database is in use
SELECT DATABASE();

-- List Databases
  -- MySQL
SHOW DATABASES;

-- Deleting a databases
DROP DATABASE record_company;
DROP DATABASE IF EXISTS sample_db;
```

### Table Commands
```SQL
-- Creating 2 new table
CREATE TABLE bands (
  id INT NOT NULL AUTO_INCREMENT, -- NOT NULL means it has to have a value
  name VARCHAR(255) NOT NULL,
  PRIMARY KEY (id) -- Sets the primary key for the table
);

CREATE TABLE albums (
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  release_year INT, -- Can have NULL values
  band_id INT NOT NULL,
  PRIMARY KEY (id),
  FOREIGN KEY (band_id) REFERENCES bands(id) -- Sets a foreign key for band_id from the id attribute/column in the bands table
);

-- Adding another column
ALTER TABLE bands
ADD another_column VARCHAR(255);

-- Deleting columns from tables
ALTER TABLE bands
DROP COLUMN another_column;

-- Showing tables
  -- MySQL
SHOW TABLES;

-- Shows the different columns and their properties
DESCRIBE table_name;

-- Deleting a table
DROP TABLE table_name;
```

### Insert Command
```SQL
-- Adding elements
INSERT INTO table_name (column_1, foreign_key)
VALUES
  ('1st element in column 1', 1),
  ('2nd element in column 1', NULL)
;
```

### Select Command
```SQL
-- Returns the whole table.
SELECT * FROM table_name;

-- Get the first 2 bands
SELECT * FROM table_name LIMIT 2;

-- Gets the 2nd element
SELECT * FROM table_name LIMIT 2,3;

-- Get from column
SELECT column_1 FROM table_name;

-- Returns the column with a different name for the column
SELECT id AS 'ID', column_1 AS 'Column 1'
FROM table_name;

-- Get elements, but ordered by a different column. If the column is a text is does by alphabetical order.
SELECT * FROM table_name ORDER BY column_1;
-- or descending order
SELECT * FROM table_name ORDER BY column_1 DESC;

-- Only get unique elements from a column
SELECT DISTINCT column_1 FROM table_name;

-- Selecting based upon a conditional
SELECT column_1 FROM table_name
WHERE id > 1;

-- Selecting text based upon wild cards
SELECT column_1 FROM table_name
WHERE column_1 LIKE '%'; -- % means any amount of characters

-- INNER JOIN ON
```

### Update Command
```SQL
-- Updating elements
UPDATE table_name
SET column_1 = 'The where command is used to specify where the SQL command will be applied to.'
WHERE id = 1;
```

### Deleting Elements
```SQL
-- Deletes the first element from a table
DELETE FROM table_name
WHERE id = 1;

-- Deletes all the rows in a table
DELETE FROM table_name;
```

### Where
Used to filter rows/elements based upon specific conditions.

| Operator | Description              |
|----------|--------------------------|
| =        | Equal to                 |
| <> or != | Not equal to             |
| <        | less than                |
| >        | greater than             |
| <=       | Less than or equal to    |
| >=       | Greater than or equal to |
| AND      | Logical and              |
| OR       | Logical or               |
| NOT      | Logical not              |
| IS NULL  | Is it equal to null      |
| BETWEEN  | BETWEEN 2000 AND 2018;   |
| LIKE     | Search for pattern.      |

#### Like
`LIKE` is used to search for a specific string pattern.

`%` means zero or more characters.

`_` means a single character.

```SQL
-- Selects all names starting with J
SELECT * FROM customers
WHERE customer_name LIKE 'J%';

-- Selects all names with 5 characters or Bob
SELECT * FROM customers
WHERE customer_name LIKE '_____' OR customer_name = 'Bob';
```

### Join

### Functions
COUNT()


## Relational Database Management System(RDBMS)
A special software program used to create and maintain a database.

Databases are usually kept on separate servers than your http endpoints(NodeJS and Express) because it is much easier to scale the database, secure the database, backup and recover the database, etc.

### MySQL
Run  `sudo mysql -u root -p`
Default port is 3306

`SOURCE schema.sql` runs a sql file

Change MySQL Password
`ALTER USER 'root'@'localhost' IDENTIFIED WITH 'mysql_native_password' BY 'new_password';`
then
`FLUSH PRIVILEGES;`

- For your local host MySQL it is recommended to make the password `root`

`exit` to exit from mysql.

Questions:
- MySQL with NodeJS
- CRUD functions
- SQL commands
- Database schema
- Seed a database
- SQL query that joins 2 tables together
- ? prepared statements
  - INSERT, UPDATE, and DELETE
- Calculation on a set of values using aggregate functions
- What are joins?
- What are views, stored procedures, and functions?


SQL is made up of 4 parts:
- Data Query Langue(DQL)
  - Used to query the database
- Data Definition Language(DDL)
  - Used to define database schemas
- Data Control Language(DCL)
  - Controlling access to the database. Permissions.
- Data Manipulation Language(DML)
  - Used for inserting, updating, and deleting.

```SQL
CREATE DATABASE record_company;
USE record_company;

CREATE TABLE bands (
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  PRIMARY KEY (id)
);

CREATE TABLE albums (
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  release_year INT,
  band_id INT NOT NULL,
  PRIMARY KEY (id),
  FOREIGN KEY (band_id) REFERENCES bands(id)
);

INSERT INTO bands (name)
VALUES
  ('Iron Maiden')
;

INSERT INTO bands (name)
VALUES
  ('Deuce'),
  ('Avenged Sevenfold'),
  ('Ankor')
;

SELECT * FROM bands; -- Outputs all of the table

insert into albums (name, release_year, band_id)
values
  ('The Number of the Beast', 1985, 1),
  ('Power Slave', 1984, 1),
  ('Nightmare', 2018, 2)
  ('Nightmare', 2010, 3),
  ('Test Album', null, 3);

select * from albums;
```