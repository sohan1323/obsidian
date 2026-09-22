
---
## SUID

**Set User ID**

Numeric value:

```
4000
```

Set SUID:

```
chmod u+s program
```

or:

```
chmod 4755 program
```

Check:

```
ls -l program
```

You may see:

```
-rwsr-xr-x
```

The `s` in the owner's execute position indicates SUID.

### Meaning

When an executable with SUID is executed, it can run with the **effective user ID of the file owner**, subject to system rules.

For example, if a program is owned by root and has SUID:

```
root
```

the program can potentially execute with effective UID 0.

This is why SUID binaries are important in Linux privilege-escalation enumeration.

Find them:

```
find / -type f -perm -4000 2>/dev/null
```

---

# SGID

**Set Group ID**

Numeric value:

```
2000
```

Set:

```
chmod g+s directory
```

or:

```
chmod 2775 directory
```

For directories, newly created files can inherit the directory's group.

Example:

```
chmod 2775 shared/
```

---

# Sticky Bit

Numeric value:

```
1000
```

Set:

```
chmod +t directory
```

or:

```
chmod 1777 directory
```

Typical example:

```
ls -ld /tmp
```

You may see:

```
drwxrwxrwt
```

The `t` indicates the sticky bit.

### Purpose

In a world-writable directory, the sticky bit restricts users from deleting/renaming files belonging to other users, subject to ownership and privilege rules.

---

# Special Permission Summary

|Permission|Octal|Common notation|
|---|---|---|
|SUID|`4000`|`s` in owner execute position|
|SGID|`2000`|`s` in group execute position|
|Sticky|`1000`|`t` in others execute position|

Example:

```
chmod 4755 program
```

means:

```
SUID + 755
```

Example:

```
chmod 2775 shared/
```

means:

```
SGID + 775
```

Example:

```
chmod 1777 shared/
```

means:

```
Sticky + 777
```

---

# Important Security Commands

Find SUID:

```
find / -type f -perm -4000 2>/dev/null
```

Find SGID:

```
find / -type f -perm -2000 2>/dev/null
```

Find world-writable files:

```
find / -type f -perm -002 2>/dev/null
```

Check permissions:

```
ls -la
```

Detailed metadata:

```
stat file.txt
```

Check ACLs:

```
getfacl file.txt
```

Check special attributes:

```
lsattr file.txt
```