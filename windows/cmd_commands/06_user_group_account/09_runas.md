
---
Runs a program using another user's credentials.

### Syntax

```
runas /user:username command
```

### Example

```
runas /user:Administrator cmd
```

Windows prompts for the specified account's password.

A new CMD process can then run under that account if authentication succeeds.

---

## Domain account

```
runas /user:DOMAIN\Admin cmd
```

or:

```
runas /user:admin@example.local cmd
```

depending on the environment.

---

## `/profile`

Load the user's profile:

```
runas /user:Administrator /profile cmd
```

---

## `/noprofile`

Don't load the user's profile:

```
runas /user:Administrator /noprofile cmd
```

---

## `/netonly`

Use supplied credentials only for remote access while the local process runs under the current account context.

```
runas /netonly /user:DOMAIN\Admin cmd
```

This is particularly relevant to domain administration and security testing, but should only be used with authorized credentials.