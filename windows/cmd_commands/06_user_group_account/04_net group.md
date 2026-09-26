
---
Manages **domain global groups**.

This differs from `net localgroup`.

### Syntax

```
net group
net group groupname
net group groupname /domain
```

### Important distinction

```
net localgroup
      ↓
Local groups

net group
      ↓
Domain groups
```

Example:

```
net group
```

On a domain-connected system, this can display domain groups.

Query a particular group:

```
net group "Domain Admins" /domain
```

This requires appropriate domain connectivity/permissions.