
---
**Purpose:** Search for a **literal string**, rather than interpreting the pattern as a regular expression.

Equivalent to:

```
grep -F
```

Example:

```
fgrep "192.168.1.10" logfile.txt
```

Modern form:

```
grep -F "192.168.1.10" logfile.txt
```

### Why useful?

Suppose your search string contains regex characters:

```
192.168.1.10
```

With regular expressions, `.` has a special meaning.

`grep -F` treats it literally.

Again, prefer:

```
grep -F
```

rather than `fgrep`.