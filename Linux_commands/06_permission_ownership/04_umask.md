
---
**Purpose:** Control the default permissions assigned when new files/directories are created.

### Syntax

```
umask [OPTION] [MODE]
```

Check current umask:

```
umask
```

Example:

```
0022
```

---

## How umask works

Typical base permissions:

### Files

```
666
```

### Directories

```
777
```

The umask removes permissions.

For:

```
umask = 022
```

New file:

```
666
-022
----
644
```

New directory:

```
777
-022
----
755
```

So:

```
touch file.txt
mkdir test
```

typically produces:

```
file.txt → 644
test/     → 755
```

---

## Set umask

```
umask 077
```

New files will typically be:

```
600
```

and directories:

```
700
```

This is useful when you want newly created files to be private by default.

---

## Important options

```
umask -S
```

Shows symbolic representation.

Example:

```
u=rwx,g=rx,o=rx
```