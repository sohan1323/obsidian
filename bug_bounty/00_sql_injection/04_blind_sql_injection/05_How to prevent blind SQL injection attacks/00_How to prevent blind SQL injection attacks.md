
---
### How to Prevent Blind SQL Injection

The primary defense against **blind SQL injection is the same as regular SQL injection: use parameterized queries (prepared statements).**

Instead of constructing SQL by concatenating user input:

```
query = "SELECT * FROM users WHERE username = '" + username + "'"
```

use a parameterized query:

```
query = "SELECT * FROM users WHERE username = %s"cursor.execute(query, (username,))
```

The database treats `username` as **data**, not as part of the SQL syntax.

### Why this prevents blind SQLi

Even if an attacker submits SQL syntax as input, the parameterized query keeps it separate from the SQL statement's structure.

```
User input
    ↓
Parameterized query
    ↓
Treated strictly as data
    ↓
Cannot alter SQL structure
```

This prevents the attacker from manipulating the query to perform boolean-based, error-based, time-based, or OAST-based SQL injection.