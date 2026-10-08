
---
### SQL Injection UNION Attacks

A **UNION attack** allows an attacker to append another `SELECT` query to the application's original SQL query and retrieve data from other tables.

Example:

```
SELECT a, b FROM table1
UNION
SELECT c, d FROM table2;
```

The result is a **single result set** containing results from both queries.

### Requirements for a UNION attack

Two conditions must be satisfied:

1. **Same number of columns**

```
SELECT a, b FROM table1
UNION
SELECT c, d FROM table2;
```

Both queries return **2 columns**.

2. **Compatible data types**

The corresponding columns must contain compatible data types.

For example:

```
First query       Second query
-----------       ------------
VARCHAR     ↔     VARCHAR
INTEGER     ↔     INTEGER
```

### Practical process

To perform a UNION-based SQLi attack, you generally need to determine:

```
Original query
      ↓
1. Find number of columns
      ↓
2. Identify columns that accept useful data types
      ↓
3. Construct compatible UNION SELECT
      ↓
4. Retrieve data from another table
```

For example, if the original query returns **2 columns** and the first column accepts text, an injected query could conceptually use:

```
UNION SELECT username, password FROM users
```

The important point is that **the injected `SELECT` must match the original query's column count and have compatible data types in corresponding positions**.