[Home](./README.md)

# Table of Contents

- [Relational Databases](#relational-databases)
  - [Atomicity Consistency Isolation Durability(ACID)](#atomicity-consistency-isolation-durabilityacid)
  - [Attribute Properties](#attribute-properties)
- [Structured Query Language(SQL)](#structured-query-languagesql)
  - [Database Commands](#database-commands)
  - [Table Commands](#table-commands)
  - [Insert Command](#insert-command)
  - [Select Command](#select-command)
  - [Update Command](#update-command)
  - [Deleting Elements](#deleting-elements)
  - [Where](#where)
    - [Like](#like)
  - [Join](#join)
    - [Inner Join](#inner-join)
    - [Left/Right Join](#leftright-join)
    - [Dereferencing](#dereferencing)
  - [Functions](#functions)
  - [Group By](#group-by)
    - [Having](#having)
  - [Alias Tables](#alias-tables)
- [Relational Database Management System(RDBMS)](#relational-database-management-systemrdbms)
  - [MySQL](#mysql)
    - [Installation](#installation)

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
  name VARCHAR(255) NOT NULL UNIQUE, -- Enforces the name column/attribute to be unique
  favorite_band INT,
  PRIMARY KEY (id), -- Sets the primary key for the table
  FOREIGN KEY (favorite_band) REFERENCES bands(id) -- Sets an internal reference
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

-- Gets column1 and column2 from table_name and adds to it the dbs and the tables in those dbs
SELECT column1, column2 FROM table_name
UNION ( -- Adds onto another query
  -- Gets all the dbs and the tables in those dbs
    -- information_schema.tables is inbuilt into SQL
  SELECT TABLE_SCHEMA AS 'databases', TABLE_NAME as 'tables' FROM information_schema.tables
  WHERE
    TABLE_SCHEMA != 'mysql' AND
    TABLE_SCHEMA != 'information_schema' AND
    TABLE_SCHEMA != 'performance_schema' AND
    TABLE_SCHEMA != 'sys'
);
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
Combines data from that row if the condition is true.

This is most often used to de-reference values.

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
Functions are almost always slower than doing checks(=, !=, >, <, etc) with hard coded data values. This is because the database can quickly find the row in which the hard coded data is in.

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
| MONTH()      | Numeric     | Gets month between 1 and 12                  |

Examples:

```SQL
-- AVG
SELECT AVG(release_year) FROM albums;
  -- 1998.5  It doesn't count null values

-- Count
SELECT COUNT(release_year) FROM albums;
  -- 4
```

## Group By
Takes all the rows and groups them by a single column. If there are 2 rows that have the same value in a column group by combines them.

This is often used with `COUNT` in order to count how many rows are in each column.

```SQL
SELECT band_id, COUNT(band_id) from albums
GROUP BY band_id;
```

This returns the table:

```
| band_id | COUNT(band_id) |
|---------|----------------|
| 1       | 2              |
| 2       | 1              |
| 3       | 1              |

```

### Having
The `HAVING` is the same as where, but happens after the `GROUP BY` so you can use data before an aggravate function.

```SQL
-- Get the number of bands with only 1 album
SELECT b.name band_name, COUNT(a.id) num_albums
FROM bands b
LEFT JOIN albums a ON b.id = a.band_id
GROUP BY b.id
HAVING num_albums = 1;
```

## Alias Tables
Alias tables are temporary names given to a table or column in order to resolve naming conflicts.

This is often used to de-reference an internal reference in a table.

```SQL
SELECT b.name AS band_name, COUNT(a.id) AS num_albums
FROM bands AS b
LEFT JOIN albums AS a;

-- You can also leave out the AS
SELECT b.name band_name, COUNT(a.id) num_albums
FROM bands b
LEFT JOIN albums a;
```

## Variables
You can have variables(user defined values) in sql by using the `@` symbol.

```SQL
SET @var = 1;

SELECT @var FROM table_name; -- Gets teh 1st column from table_name
```

## Indexes
Indexes are used to speed up queries.

```SQL
CREATE INDEX index_name ON table_name (column1, column2);
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

# Object Relational Mappings(ORMs)
ORMs are used to interact with relational databases using oop.

## Sequelize
Sequelize can work with multiple different RDBMS so you need to insteall `mysql2` as well if you are using mysql.

```javascript
const Sequelize = require("sequelize")
let sequelize

if(process.env.JAWSDB_URL){
  // Connection provided by JAWSDB_URL which is what Heroku uses
  sequelize = Sequelize(process.env.JAWSDB_URL)
}else{
  // Create the db before using sequelize
  sequelize = new Sequelize(`db_name`, `username`, `password`, {
    // Customize connection with object
    host: `localhost`, // This is set by default
    port: 3306, // This is set by default
    dialect: `mysql` // Which SQL DB Server
  })
}

module.exports = sequelize // ./connection
```

### Syncing
Syncing is connecting to your sql server with sequelize.

In your server file:

```javascript
// Express code
const sequelize = require(`./connection`)
const PORT = 3000

// Connect to the db before running server
sequelize.sync().then(() => {
  app.listen(PORT)
})

// or you can force true to drop and recreate tables on every sync based upon your modals.
  // DO NOT use this when deploying an app. Your data in your db will be destroyed.
sequelize.sync({force: true}).then(() => {
  app.listen(port)
})

```

### Modals
Modals are JS classes that define a table's schema.

```javascript
const { Model, DataTypes } = require('sequelize')
const sequelize = require('..config/connection') // Get the connection

class Book extends Model{}

Book.init(
  { // First object are the columns
    columnName: { // If you don't set a primary key sequelize will set one automatically as "id"
      type: DataTypes.STRING, // SQL type
      allowNull: false,
      primaryKey: true,
      autoIncrement: true
    },
    column2: {
      type: DataTypes.INTEGER
    },
  },
  {
    sequelize, // Link to db
    timestamps: false, // Don't set timeouts
    underscore: true, // Converts Camel case to snake case when putting it in the db
    modelName: `book` // table name
  }
)

module.exports = Book
```

```javascript
// In the server code add
const Book = require(`./Book`) // This invokes the init method and thus connect to sequelize.
```

### Seeding data
Seeding data is putting data into the database.

```javascript
const Book = require(`./book`)

// Creating a new row
Book.create({
  column1: `column1`,
  column2: `column2`
})

// Creating multiple new rows
Book.bulkCreate([
  {
    column1: `column1`,
    column2: `column2`
  },
  {
    column1: `column1`,
    column2: `column2`
  }
])
```

You need to `npm install sequelize-cli`

Creating a new seeder file in the seeders folder.
`npx sequelize-cli seed:generate --name seed-name`

The sequelize seed file where you data is stored:

```javascript
'use strict'; // Activates strict mode for this file which throws more errors.

module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.bulkInsert('table_name', [
      { column1: 'value1', column2: 'value2', ... },
      { column1: 'value3', column2: 'value4', ... },
      // More data entries...
    ], {});
  },

  down: (queryInterface, Sequelize) => {
    // Removes all data from a a table
    return queryInterface.bulkDelete('table_name', null, {});
  }
};
```

Seeding data: `npx sequelize-cli db:seed:all`

Undoing the seeded data: `npx sequelize-cli db:seed:undo:all`

### Querying data

```javascript
Book.findAll({
  order: ['tit;e'],
  where: {
    is_paperbakc: true
  },
}).then((bookData))

Book.findByPK // finds by primary key
Book.findOne

.update({
  // info
},{
  where: {
    isbn: 
  }
})
.then(updatedBook => res.json(updatedBook))
.catch(error => res.json(error))

Book.destroy
```