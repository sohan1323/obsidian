
---
Although introduced earlier, it is relevant to network/domain administration.

```
net accounts
```

Shows local account policy.

Useful options include:

```
net accounts /minpwlen:12
```

Minimum password length:

```
net accounts /minpwlen:12
```

Maximum password age:

```
net accounts /maxpwage:90
```

Lockout threshold:

```
net accounts /lockoutthreshold:5
```

These settings are particularly relevant when auditing Windows account security.