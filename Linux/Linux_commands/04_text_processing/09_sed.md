
---
**Purpose:** Stream editor used to **search, replace, delete, and transform text**.

This is one of the most important Linux commands to master.

### Syntax

```
sed [OPTIONS] 'COMMAND' FILE
```

---

## `s` — substitute

```
sed 's/old/new/' file.txt
```

Replaces the first occurrence of `old` on each line.

Replace all occurrences:

```
sed 's/old/new/g' file.txt
```

Ignore case:

```
sed 's/old/new/gi' file.txt
```

---

## Modify a specific line

Replace on line 3:

```
sed '3s/old/new/' file.txt
```

Replace lines 2–5:

```
sed '2,5s/old/new/g' file.txt
```

---

## Delete lines

Delete line 3:

```
sed '3d' file.txt
```

Delete lines 2–5:

```
sed '2,5d' file.txt
```

Delete empty lines:

```
sed '/^$/d' file.txt
```

---

## Print specific lines

```
sed -n '5p' file.txt
```

Print lines 5–10:

```
sed -n '5,10p' file.txt
```

---

## Edit the file directly

```
sed -i 's/old/new/g' file.txt
```

### Backup before modification

```
sed -i.bak 's/old/new/g' file.txt
```

This creates:

```
file.txt
file.txt.bak
```

### Practical cybersecurity use

Modify configuration files:

```
sed -i 's/^PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config
```

Always understand exactly what a command changes before applying it to system configuration.