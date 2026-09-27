
---
**Purpose:** Display the contents of a file.

### Syntax

```
cat [OPTION]... [FILE]...
```

### Important options

|Option|Meaning|
|---|---|
|`-n`|Number all lines|
|`-b`|Number non-empty lines|
|`-s`|Suppress repeated empty lines|
|`-A`|Show non-printing characters|
|`-E`|Show `$` at end of lines|
|`-T`|Show tabs as `^I`|

### Examples

Display a file:

```
cat file.txt
```

Display multiple files:

```
cat file1.txt file2.txt
```

Number lines:

```
cat -n file.txt
```

Number only non-empty lines:

```
cat -b file.txt
```

Show tabs and line endings:

```
cat -A file.txt
```

### Combining files

```
cat file1.txt file2.txt > combined.txt
```

This creates `combined.txt` containing both files.

Append instead:

```
cat file3.txt >> combined.txt
```

### Practical use

Read configuration files:

```
cat /etc/hosts
```

```
cat /etc/passwd
```

For small files, `cat` is convenient. For large files, use `less`.