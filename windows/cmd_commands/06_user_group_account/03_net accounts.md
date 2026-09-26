
---
Displays or modifies local account/password policy.

### Basic

```
net accounts
```

You may see:

```
Minimum password age
Maximum password age
Minimum password length
Length of password history maintained
Lockout threshold
Lockout duration
Lockout observation window
```

---

## Set minimum password length

```
net accounts /minpwlen:12
```

---

## Set maximum password age

```
net accounts /maxpwage:90
```

---

## Set minimum password age

```
net accounts /minpwage:1
```

---

## Password history

```
net accounts /uniquepw:5
```

Requires the user to use passwords different from the specified number of previous passwords.

---

## Account lockout threshold

```
net accounts /lockoutthreshold:5
```

Be careful when changing authentication policies on production systems.