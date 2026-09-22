
---
**Purpose:** Search for lines matching a pattern.

### Syntax

```
grep [OPTIONS] PATTERN [FILE...]
```

Basic example:

```
grep "error" logfile.txt
```

This prints lines containing `error`.

---

## Important options

|Option|Meaning|
|---|---|
|`-i`|Ignore case|
|`-v`|Invert match|
|`-n`|Show line numbers|
|`-r` / `-R`|Search recursively|
|`-l`|Show filenames containing matches|
|`-L`|Show filenames without matches|
|`-c`|Count matching lines|
|`-w`|Match whole words|
|`-x`|Match entire line|
|`-o`|Print only matching portion|
|`-E`|Extended regular expressions|
|`-F`|Fixed string search|
|`-A N`|Show N lines after match|
|`-B N`|Show N lines before match|
|`-C N`|Show N lines around match|
|`-h`|Hide filenames|
|`-H`|Show filenames|
|`-q`|Quiet mode|

---

## Examples

Case-insensitive:

```
grep -i "error" logfile.txt
```

Find lines that **don't** contain `error`:

```
grep -v "error" logfile.txt
```

Show line numbers:

```
grep -n "error" logfile.txt
```

Recursive search:

```
grep -r "password" /etc
```

Show only filenames:

```
grep -rl "password" /etc
```

Count matching lines:

```
grep -c "failed" auth.log
```

Whole-word matching:

```
grep -w "root" /etc/passwd
```

Show only matching text:

```
grep -o "192.168.1.10" logfile.txt
```

Show context:

```
grep -C 3 "error" logfile.txt
```

This shows three lines before and after the match.

---

## Multiple patterns

```
grep -E "error|warning|failed" logfile.txt
```

Search recursively while ignoring case:

```
grep -ri "password" /var/log
```

### Practical cybersecurity examples

Find failed SSH authentication:

```
grep "Failed password" /var/log/auth.log
```

Find successful SSH logins:

```
grep "Accepted" /var/log/auth.log
```

Search configuration files:

```
grep -ri "password" /etc
```

Find IP addresses in a log:

```
grep -Eo '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' access.log
```