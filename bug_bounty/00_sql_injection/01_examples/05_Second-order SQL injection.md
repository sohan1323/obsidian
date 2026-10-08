
---
### SQLi Example — Second-Order SQL Injection

**Second-order SQL injection** occurs when an attacker-controlled value is **stored by the application first**, and the stored value is later retrieved and used unsafely in another SQL query.

### Example

Suppose an application allows users to set their username:

```
username = attacker-controlled input
```

The application safely stores it in the database:

```
INSERT INTO users (username)
VALUES ('attacker_input');
```

Later, an administrator searches for that username. The application retrieves the stored value and unsafely constructs another query:

```
SELECT * FROM users
WHERE username = '$stored_username';
```

If the stored value contains SQL syntax, it can become active when used in this second query.

### Attack flow

```
Attacker input
      ↓
Stored in database
      ↓
Later retrieved by application
      ↓
Inserted unsafely into another SQL query
      ↓
SQL injection occurs
```

The important distinction is that **the injection does not necessarily occur when the value is initially submitted**. It occurs later when the previously stored value is reused in an unsafe SQL query.

**Key idea:** First-order SQLi = injection is executed immediately.  
Second-order SQLi = malicious input is stored first and executed later.