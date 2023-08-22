[Home](./README.md)

# Structured Query Language(SQL)
SQL is a language used to interact with relational databases.

Relational databases organize things into tables with each element in the tabe having a unique id. Elements in these tables can connect to elements from other tables by having a column of that connection's unique id.

Table 1

| user_id | username | email               |
|---------|----------|---------------------|
| 1       | user123  | user123@example.com |
| 2       | alice    | alice@example.com   |
| 3       | bob      | bob@example.com     |


Table 2

| post_id | user_id | message      |
|---------|---------|--------------|
| 1       | 1       | Hello World  |
| 2       | 2       | My Thoughts  |
| 3       | 1       | Another Post |

## Relational database management system
### MySQL

Questions:
  - What are schemas?
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