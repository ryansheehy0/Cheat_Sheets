[Home](./README.md)

# Relational Databases
Relational databases organize things into tables with each element in the table having a unique id/primary key. Elements in these tables can connect to elements from other tables by having a column of that connection's unique id.

Rows are elements and columns are attributes. Each cell contains one value of a specific data type.

- A surrogate key is a unique id that has no mapping to anything in the real world. It is just used internally in the db.
- A natural key is a unique attribute that has a real world mapping to something in the real world. Like a unique email address.
- A foreign key is an attribute on a table that links to a unique key of another table.
- A composite key is a primary key that is made up of 2 attributes. Only both of the attributes can uniquely identify an element.

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

- A schema refers to how the database is layed out. The structure or design of the database.
- A query is a search in the database in order to read information.
- Create Read Update Delete(CRUD) are the 4 main operation when dealing with databases.

## Structured Query Language(SQL)
SQL is a language used to interact with relational databases.

SQL is not case sensitive, however capital letters for the commands are recommended.

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
-- Creating databases
CREATE DATABASE database_name;
```

```SQL
-- Deleting databases
DROP DATABASE database_name;
```

| Data Types | Description                                                           |
|------------|-----------------------------------------------------------------------|
| INT        |                                                                       |
| FLOAT      |                                                                       |
| VARCHAR(#) | Strings with a pre-defined length. Cannot exceed the # of characters. |
| TEXT       | Strings of undefined length.                                          |

When using TEXT always run a delete or update with a select and where clause. Otherwise, it might mess the whole database.

Data Types apply to the column.

Columns may also have constraints like
- unique
- not null
- primary key
- enum

### Data Query Langue(DQL)
```SQL
-- Gets data from the database
SELECT employee.name, employee.age;
FROM employee;
WHERE employee.salary > 30000;
```

### Relational Database Management System(RDBMS)
A special software program used to create and maintain a database.

Databases are usually kept on separate servers than your http endpoints(NodeJS and Express) because it is much easier to scale the database, secure the database, backup and recover the database, etc.
#### MySQL

Questions:
- MySQL
- CRUD functions
- SQL commands
- Create and delete databases
- Create a table to store data
- NodeJS to connect to MySQL
- Data types for each column
- Database schema
- Seed a database
- Tables with primary and foreign keys
- SQL query that joins 2 tables together
- ? prepared statements
  - INSERT, UPDATE, and DELETE
- Calculation on a set of values using aggregate functions
- What are joins?
- What are tables, views, indexes, and other objects?

### Atomicity Consistency Isolation Durability(ACID)
One of the fundamental guarantees a transaction(Sequence of CRUDs) must satisfy for a database.

Atomicity means that a transaction either executes entirely or not at all. If part of the transaction doesn't work then the database is no changed.

Consistency is 

Isolation is 