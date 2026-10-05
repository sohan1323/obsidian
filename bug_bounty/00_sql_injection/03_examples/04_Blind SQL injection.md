
---
### SQLi Example — Blind SQL Injection

**Blind SQL injection** occurs when the application is vulnerable to SQL injection, but **does not directly display the results of the injected SQL query**.

Suppose the application has:

```
GET /product?id=10
```

The backend executes:

```
SELECT * FROM products WHERE id = 10;
```

An attacker tests two conditions:

```
10 AND 1=1
```

and:

```
10 AND 1=2
```

If the application responds differently:

- `1=1` → normal product page
- `1=2` → product not found

the attacker can infer that the SQL condition is being evaluated, even though the database output is not directly displayed.

The attacker can then ask **true/false questions** about database information.

For example:

```
10 AND (SELECT COUNT(*) FROM users) > 0
```

If the normal response occurs, the condition is likely true, indicating that the `users` table contains at least one row.

### Types of Blind SQLi

1. **Boolean-based blind SQLi** — infer information from differences between true and false responses.
2. **Time-based blind SQLi** — infer information from differences in response time.

**Key idea:** The attacker doesn't directly see the SQL query's output; they **infer information from observable behavior**.