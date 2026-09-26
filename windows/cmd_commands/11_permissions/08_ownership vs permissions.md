
---
This distinction is critical.

Suppose:

```
Alice
```

owns:

```
C:\Lab
```

but the ACL doesn't give Alice access.

Ownership does **not** automatically mean unrestricted file access.

The owner has the ability to modify the object's permissions, subject to Windows security rules.

Conceptually:

```
Owner
  ↓
Can manage security descriptor
  ↓
DACL
  ↓
Effective access
```