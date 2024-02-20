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