
---
### Blind SQL Injection

**Blind SQL injection** occurs when an application is vulnerable to SQL injection, but the HTTP response **does not directly contain the results of the injected SQL query or useful database error messages**.

For example, an application may respond only with:

```
Product found
```

or:

```
Product not found
```

without showing the database's output.

### Why UNION attacks may not work

A typical `UNION` attack depends on seeing the injected query's results:

```
UNION SELECT username, password FROM users
```

If the application doesn't display those results, the attacker cannot directly see the returned data.

### How blind SQLi works

Instead, the attacker uses **indirect signals** to infer information.

For example:

```
AND 1=1
```

might produce:

```
Product found
```

while:

```
AND 1=2
```

might produce:

```
Product not found
```

The attacker can use these differences to ask the database **true/false questions** and gradually infer information.

Common blind SQLi techniques are:

1. **Boolean-based SQLi** — infer data from differences in application responses.
2. **Time-based SQLi** — infer data from differences in response times.
3. **Out-of-band SQLi** — retrieve information through a separate network interaction.

**Key idea:** In normal SQLi, you can **see the database output**. In blind SQLi, you **infer the database output indirectly**.