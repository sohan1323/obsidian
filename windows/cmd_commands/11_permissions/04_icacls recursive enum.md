
---
Use `/T` to process files and subdirectories recursively.

```
icacls C:\Lab /T
```

Example:

```
icacls C:\Users\Public /T
```

This is useful when auditing an entire directory tree.

# `/C`

Continue even when errors occur.

```
icacls C:\Lab /T /C
```

Without `/C`, some errors can interrupt processing.


# `/Q`

Suppresses success messages.

```
icacls C:\Lab /T /Q
```

Useful when processing large directory trees.


# `/L`

Operate on the symbolic link itself rather than its target.

```
icacls C:\Lab\MyLink /L
```

This matters when auditing symbolic links.


# `/S`

Replaces ACLs on files while preserving inheritance behavior.

This is an advanced ACL operation.

```
icacls C:\Lab /S
```

For normal permission inspection, you generally won't need it.


# `/RESET`

Resets ACLs to inherited defaults.

```
icacls C:\Lab /reset /T
```

This can significantly alter permissions, so only use it when you intentionally want to restore ACL inheritance.


# `/grant`

### Syntax

```
icacls Path /grant User:Permission
```

Example:

```
icacls C:\Lab /grant Alice:R
```

Give Modify:

```
icacls C:\Lab /grant Alice:M
```

Give Full Control:

```
icacls C:\Lab /grant Alice:F
```