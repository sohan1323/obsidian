
---
### Extracting Sensitive Data via Verbose SQL Error Messages

Sometimes a database is configured to return **detailed error messages**. These errors can reveal information about the SQL query and, in some cases, the **actual data returned by the database**.

### 1. Discovering the SQL query

Suppose you submit:

```
'
```

and receive:

```
Unterminated string literal started at position 52 in SQL
SELECT * FROM tracking WHERE id = '''.
Expected char
```

This reveals that:

```
SELECT * FROM tracking WHERE id = '...'
```

The error tells you:

- The approximate SQL query structure
- That the input is inside a **quoted string**
- That your quote disrupted the SQL syntax

This information helps understand the injection context.

---

### 2. Extracting data through an error

Sometimes you can deliberately cause a **type-conversion error** that contains the value you're trying to retrieve.

For example:

```
CAST(
    (SELECT example_column FROM example_table)
    AS int
)
```

If `example_column` contains:

```
Example data
```

but the database expects an integer, the conversion fails:

```
ERROR: invalid input syntax for type integer: "Example data"
```

The important part is:

```
"Example data"
```

The database has included the **actual data value inside the error message**.

### Attack flow

```
SQL injection
     ↓
Execute expression returning sensitive data
     ↓
Force incompatible type conversion
     ↓
Database generates error
     ↓
Error contains the returned data
     ↓
Data becomes visible to attacker
```

### Key idea

Verbose errors can turn an otherwise **blind SQL injection** into something closer to **visible SQL injection**, because the database itself leaks information through its error message.