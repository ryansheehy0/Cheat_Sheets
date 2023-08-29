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
| DECIMAL                | Store fixed point decimal numbers. Often used for monetary values. |

You can specify a default value.
```SQL
time DATETIME DEFAULT CURRENT_TIMESTAMP,
```

When using TEXT always run a delete or update with a select and where clause. Otherwise, it might mess the whole database.

VARCHAR(255) is often used over TEXT because it takes up less space.

# Structured Query Language(SQL)
SQL is a language used to interact with relational databases. Tends to retrieve data very fast.

- SQL keywords are not case sensitive, however capital letters for the commands are recommended.
- Table names and column names tend to be put in lowercase with underscores instead of spaces.
- Strings are put inside single quotes. 's
- Commands in SQL end in semi-columns. ;s
- `--`s are used for comments in SQL

## Database Commands
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

-- In your schema.sql you usually run this at the beginning
DROP DATABASE IF EXISTS sample_db;
CREATE DATABASE sample_db;
```

## Table Commands
```SQL
-- Creating 2 new table
CREATE TABLE bands (
  id INT NOT NULL AUTO_INCREMENT, -- NOT NULL means it has to have a value
  name VARCHAR(255) NOT NULL,
  favorite_band INT,
  PRIMARY KEY (id), -- Sets the primary key for the table
  FOREIGN KEY (favorite_band) REFERENCES bands(id), -- Sets an internal reference
  UNIQUE (name) -- Enforces the name column/attribute to be unique
);

CREATE TABLE albums (
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, -- You can also create a primary key inline
  name VARCHAR(255) NOT NULL,
  release_year INT, -- Can have NULL values
  band_id INT NOT NULL,
  FOREIGN KEY (band_id) REFERENCES bands(id), -- Sets a foreign key for band_id from the id attribute/column in the bands table
  ON DELETE SET NULL -- When something is deleted it is set to null
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

## Insert Command
```SQL
-- Adding elements
INSERT INTO table_name (column_1, foreign_key)
VALUES
  ('1st element in column 1', 1),
  ('2nd element in column 1', NULL);
```

## Select Command
```SQL
-- Returns the whole table.
SELECT * FROM table_name;

-- Get the first 2 bands
SELECT * FROM table_name LIMIT 2;

-- Gets the 2nd element
SELECT * FROM table_name LIMIT 1,1; -- Limit offset, count

-- Get from column
SELECT column_1 FROM table_name;
SELECT column_1, column_2 FROM table_name;

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
```

## Update Command
```SQL
-- Updating elements
UPDATE table_name
SET column_1 = 'name'
WHERE id = 1;
```

## Deleting Elements
```SQL
-- Deletes the first element from a table
DELETE FROM table_name
WHERE id = 1;

-- Deletes all the rows in a table
DELETE FROM table_name;
```

## Where
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

### Like
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

## Join
The JOIN command, when used with SELECT, returns the rows of 2 or more tables that match the conditional. The output combines/joins those rows together into one table.

Ex:

bands table

| id | name                |
|----|---------------------|
| 1  | 'Iron Maiden'       |
| 2  | 'Deuce'             |
| 3  | 'Avenged Sevenfold' |
| 4  | 'Ankor'             |

albums table

| id | name                      | release_year | band_id |
|----|---------------------------|--------------|---------|
| 1  | 'The Number of the Beast' | 1982         | 1       |
| 2  | 'Power Slave'             | 1984         | 1       |
| 3  | 'Nightmare'               | 2018         | 2       |
| 4  | 'Nightmare'               | 2010         | 3       |

### Inner Join
Combines data from that row if the condition matches for both the left(first) table and the right(second) table.
Combines data from that row if the condition is true fro both the left(first) table and the right(second) table.

```SQL
SELECT * from bands
INNER JOIN albums ON bands.id = albums.band_id;
-- This is also the same as
  -- JOIN albums ON bands.id = albums.band_id;
```

This returns the table:

```
[ From bands               ][ From albums                                            ]

| id | name                | id | name                      | release_year | band_id |
|----|---------------------|----|---------------------------|--------------|---------|
| 1  | 'Iron Maiden'       | 1  | 'The Number of the Beast' | 1982         | 1       |
| 1  | 'Iron Maiden'       | 2  | 'Power Slave'             | 1984         | 1       |
| 2  | 'Deuce'             | 3  | 'Nightmare'               | 2018         | 2       |
| 3  | 'Avenged Sevenfold' | 4  | 'Nightmare'               | 2010         | 3       |
```

### Left/Right Join
**Left join** prints out everything in the left(first) table and if the condition is true it also prints for the right(second table). If the condition is false it returns null for those values.

**Right join** prints out everything in the right(second) table and if the condition is true it also prints for the left(first table). If the condition is false it returns null for those values.

```SQL
SELECT * from bands
LEFT JOIN albums ON bands.id = albums.band_id;
```

This returns the table:

```
[ From bands               ][ From albums                                              ]

| id | name                | id   | name                      | release_year | band_id |
|----|---------------------|------|---------------------------|--------------|---------|
| 1  | 'Iron Maiden'       | 1    | 'The Number of the Beast' | 1982         | 1       |
| 1  | 'Iron Maiden'       | 2    | 'Power Slave'             | 1984         | 1       |
| 2  | 'Deuce'             | 3    | 'Nightmare'               | 2018         | 2       |
| 3  | 'Avenged Sevenfold' | 4    | 'Nightmare'               | 2010         | 3       |
| 4  | 'Ankor'             | null | null                      | null         | null    |
```

### Dereferencing
You can use join to dereference references. Whenever you have columns with the same name for different tables you need to specify which one you are referring to.

```SQL
SELECT albums.id, albums.name, release_year AS 'release year', bands.name
FROM albums
JOIN bands ON albums.band_id = bands.id;
```

This returns the table:

```
| id   | name                      | release year | name                |
|------|---------------------------|--------------|---------------------|
| 1    | 'The Number of the Beast' | 1982         | 'Iron Maiden'       |
| 2    | 'Power Slave'             | 1984         | 'Iron Maiden'       |
| 3    | 'Nightmare'               | 2018         | 'Deuce'             |
| 4    | 'Nightmare'               | 2010         | 'Avenged Sevenfold' |
```

## Functions

| Name         | Type        | Description                                  |
|--------------|-------------|----------------------------------------------|
| CONCAT()     | String      | Concatenates 2 or more strings               |
| UPPER()      | String      | Converts string to uppercase                 |
| LOWER()      | String      | Converts string to lowercase                 |
| LENGTH()     | String      | Gets the length of the string                |
| SUM()        | Numeric     | Calculates the sum of numbers                |
| AVG()        | Numeric     | Calculates the average of numbers            |
| COUNT()      | Numeric     | Counts the number of rows or non-null values |
| MIN()        | Numeric     | Finds the minimum value in a column          |
| MAX()        | Numeric     | Finds the maximum value in a column          |
| DATEPART()   | Date/Time   | Extracts a specific part from a date or time |
| DATEDIFF()   | Date/Time   | Calculates the difference between two dates  |
| CASE         | Conditional | Performs conditional logic                   |
| COALESCE()   | Conditional | Returns the first non-null value in a list   |
| GROUP BY     | Aggregation | Groups rows based on one or more columns     |
| HAVING       | Aggregation | Filters aggregated results                   |
| ORDER BY     | Aggregation | Sorts the result set                         |
| ROW_NUMBER() | Window      | Assigns a unique row number to each row      |
| LAG()        | Window      | Accesses the value of a previous row         |

Examples:

```SQL
-- AVG
SELECT AVG(release_year) FROM albums;
  -- 1998.5  It doesn't count null values

-- Count
SELECT COUNT(release_year) FROM albums;
  -- 4
```


# Relational Database Management System(RDBMS)
A special software program used to create and maintain a database.

Databases are usually kept on separate servers than your http endpoints(NodeJS and Express) because it is much easier to scale the database, secure the database, backup and recover the database, etc.

## MySQL
The default port for MySQL is 3306.


`SOURCE schema.sql` allows you to run a sql file in MySQL.

### Installation
1. `sudo apt update`
1. `sudo apt install mysql-server`
1. `sudo mysql -u root -p`
1. Change the default mysql password
  - For your local host root it is recommended to make the password `root`
  - `ALTER USER 'root'@'localhost' IDENTIFIED WITH 'mysql_native_password' BY 'new_password';`
  - `FLUSH PRIVILEGES;`
  - `exit`
1. Now you can run `mysql -u root -p` to start you mysql server in the future


Questions:
- MySQL with NodeJS
- ? prepared statements
  - INSERT, UPDATE, and DELETE
- What are views, stored procedures?