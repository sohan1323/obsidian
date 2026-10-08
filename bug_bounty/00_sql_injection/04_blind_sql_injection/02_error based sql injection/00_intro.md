
---
### Error-Based SQL Injection

**Error-based SQL injection** is a technique where SQL errors are deliberately triggered and the application's error response is used to **infer or extract information from the database**.

There are two main forms:

### 1. Conditional errors

You trigger an error depending on whether a SQL condition is **true or false**.

Conceptually:

```
Condition TRUE  → SQL error occurs
Condition FALSE → No SQL error
```

By observing whether an error occurs, you can use the same **true/false inference approach** as boolean-based blind SQLi.

For example:

```
Injected condition
       ↓
Database evaluates it
       ↓
TRUE  → Error response
FALSE → Normal response
```

This allows information to be extracted one piece at a time.

### 2. Verbose SQL errors

Some database errors may directly include the **result of a SQL expression**.

For example, if an error message exposes a value returned by a query, an otherwise blind SQL injection can effectively become **visible SQL injection**.

Conceptually:

```
SQL query
   ↓
Database error
   ↓
Error message contains database value
   ↓
Attacker reads the value
```

### Key distinction

| Type                               | Information comes from                  |
| ---------------------------------- | --------------------------------------- |
| **Boolean-based blind SQLi**       | Different normal responses              |
| **Error-based SQLi — conditional** | Different error/no-error responses      |
| **Error-based SQLi — verbose**     | Data exposed directly in error messages |