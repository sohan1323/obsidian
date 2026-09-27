
---
**Purpose:** Change file or directory permissions.

### Syntax

```
chmod [OPTION] MODE FILE...
```

There are two major ways to specify permissions:

- **Symbolic mode**
- **Numeric/octal mode**

---

## Understanding permissions first

Run:

```
ls -l file.txt
```

Example:

```
-rwxr-xr-- 1 alice developers 1200 Sep 22 15:00 file.txt
```

The permission section is:

```
-rwxr-xr--
```

Break it down:

```
-   rwx   r-x   r--
    │     │     │
    │     │     └── others
    │     └──────── group
    └────────────── owner
```

Permissions:

|Symbol|Meaning|
|---|---|
|`r`|Read|
|`w`|Write|
|`x`|Execute|
|`-`|Permission absent|

---

## Numeric permissions

Each permission has a value:

|Permission|Value|
|---|---|
|`r`|4|
|`w`|2|
|`x`|1|

Therefore:

```
rwx = 4 + 2 + 1 = 7
rw- = 4 + 2 = 6
r-x = 4 + 1 = 5
r-- = 4
-wx = 2 + 1 = 3
-w- = 2
--x = 1
--- = 0
```

For example:

```
rwxr-xr--
```

becomes:

```
rwx = 7
r-x = 5
r-- = 4
```

Therefore:

```
chmod 754 file.txt
```

---

## Symbolic mode

### Add permission

Add execute permission for owner:

```
chmod u+x script.sh
```

Add execute permission for group:

```
chmod g+x script.sh
```

Add execute permission for others:

```
chmod o+x script.sh
```

Add execute for everyone:

```
chmod a+x script.sh
```

---

### Remove permission

Remove write permission from others:

```
chmod o-w file.txt
```

Remove execute from group:

```
chmod g-x script.sh
```

Remove write from everyone:

```
chmod a-w file.txt
```

---

### Set exact symbolic permissions

```
chmod u=rwx,g=rx,o=r file.txt
```

Equivalent to:

```
754
```

---

## Numeric mode

Owner read/write:

```
chmod 600 file.txt
```

Result:

```
rw-------
```

Typical private SSH key permission:

```
chmod 600 ~/.ssh/id_rsa
```

Owner read/write, everyone else read:

```
chmod 644 file.txt
```

Executable script:

```
chmod 755 script.sh
```

Private directory:

```
chmod 700 private/
```

---

## Recursive permissions

```
chmod -R 755 directory/
```

`-R` means recursive.

⚠️ Be careful with recursive permission changes, particularly under `/etc`, `/usr`, `/var`, or `/`.

---

## Important options

|Option|Meaning|
|---|---|
|`-R`|Recursive|
|`-v`|Verbose|
|`-c`|Report only when changes occur|
|`-f`|Suppress most errors|
|`--reference=FILE`|Copy permissions from another file|

Example:

```
chmod --reference=file1.txt file2.txt
```