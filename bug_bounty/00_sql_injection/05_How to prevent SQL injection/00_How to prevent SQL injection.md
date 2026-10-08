
---
### How to Prevent SQL Injection

The primary defense is to use **parameterized queries (prepared statements)** instead of concatenating user input into SQL statements.

### Vulnerable code

```
String query =
    "SELECT * FROM products WHERE category = '" + input + "'";

Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery(query);
```

Here, `input` becomes part of the SQL statement itself, so an attacker can potentially modify the query's structure.

### Safe code

```
PreparedStatement statement =
    connection.prepareStatement(
        "SELECT * FROM products WHERE category = ?"
    );

statement.setString(1, input);

ResultSet resultSet = statement.executeQuery();
```

Here:

```
SQL structure → fixed
User input    → parameter/data
```

The input cannot modify the structure of the SQL query.

### Where parameterized queries work

They can be used when untrusted input represents **data**, such as:

```
WHERE username = ?
```

```
INSERT INTO users (username) VALUES (?)
```

```
UPDATE users SET email = ? WHERE id = ?
```

### Where parameterization doesn't work

Parameters generally cannot represent SQL identifiers or syntax elements such as:

```
SELECT * FROM ?
```

```
SELECT ? FROM users
```

```
SELECT * FROM users ORDER BY ?
```

For these cases, use a **strict allowlist** of permitted values or redesign the query logic.

For example:

```
String[] allowed = {"name", "price", "date"};
```

Only values from the predefined allowlist should be accepted.

### Important rule

The SQL query passed to the database should be a **hard-coded constant** containing no variable data:

```
Hard-coded SQL + parameters → Safe
Dynamic SQL + string concatenation → Risky
```

Do not assume particular input is "trusted" and therefore safe to concatenate. Data can originate from unexpected sources or become attacker-controlled later as the application changes.