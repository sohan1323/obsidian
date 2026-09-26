
---
You can specify multiple permissions.

Example:

```
icacls C:\Lab /grant Alice:RX
```

This grants:

```
Read
+
Execute
```


# Grant Inheritance

You can specify inheritance behavior.

Example:

```
icacls C:\Lab /grant Alice:(OI)(CI)M
```

Meaning:

```
OI = Object inherit
CI = Container inherit
M  = Modify
```

This is commonly used when applying permissions to a directory tree.



# `/grant:r`

`/grant:r` replaces previously explicitly granted permissions for that user.

```
icacls C:\Lab /grant:r Alice:R
```

This is different from simply adding another ACE.


# `/deny`

Explicitly denies a permission.

```
icacls C:\Lab /deny Alice:W
```

This denies write access.

Another example:

```
icacls C:\Lab /deny Alice:M
```

**Use explicit deny carefully.**

Windows permission evaluation can become confusing when users belong to multiple groups.


# `/remove`

Removes an ACL entry.

```
icacls C:\Lab /remove Alice
```

This removes explicit ACL entries for Alice.


# `/remove:g`

Removes grant entries.

```
icacls C:\Lab /remove:g Alice
```

# `/remove:d`

Removes deny entries.

```
icacls C:\Lab /remove:d Alice
```


# `/inheritance`

Controls inheritance.

### Enable inheritance

```
icacls C:\Lab /inheritance:e
```

### Disable inheritance but copy inherited permissions

```
icacls C:\Lab /inheritance:d
```

### Disable inheritance and remove inherited permissions

```
icacls C:\Lab /inheritance:r
```

Important distinction:

```
/e = enable
/d = disable
/r = remove inherited permissions
```



# Save ACLs — `/save`

Save ACL information to a file.

```
icacls C:\Lab /save C:\Backup\lab-acls.txt /T
```

This is useful for ACL backup/auditing.



# Restore ACLs — `/restore`

Restore previously saved ACL information.

```
icacls C:\Lab /restore C:\Backup\lab-acls.txt
```

Use this carefully because it changes permissions.



# `/findsid`

Find objects whose ACLs contain a specified SID.

```
icacls C:\Lab /findsid S-1-5-21-...
```

Useful during security auditing.



# `/substitute`

Substitutes one SID for another in ACL information.

```
icacls C:\Lab /substitute OldSID NewSID
```

This is an advanced administrative operation.