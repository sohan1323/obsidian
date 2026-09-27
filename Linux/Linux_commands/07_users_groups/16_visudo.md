
---
**Purpose:** Safely edit the sudoers configuration.

### Syntax

```
sudo visudo
```

The configuration is commonly:

```
/etc/sudoers
```

### Why use `visudo`?

Do **not** casually edit `/etc/sudoers` using:

```
sudo nano /etc/sudoers
```

`visudo` checks the syntax before saving, reducing the risk of breaking sudo configuration.

### Example rule

A rule conceptually like:

```
alice ALL=(ALL) ALL
```

allows Alice to use sudo according to that rule.

### Important

Sudo configuration is security-sensitive. A small configuration mistake can grant excessive privileges or prevent administrators from using sudo.