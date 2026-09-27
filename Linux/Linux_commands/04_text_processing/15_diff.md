
---
**Purpose:** Show differences between files.

### Syntax

```
diff [OPTIONS] FILE1 FILE2
```

### Example

```
diff file1.txt file2.txt
```

Unified format:

```
diff -u file1.txt file2.txt
```

Recursive directory comparison:

```
diff -r directory1 directory2
```

### Important options

|Option|Meaning|
|---|---|
|`-u`|Unified format|
|`-c`|Context format|
|`-r`|Recursive|
|`-q`|Only say whether files differ|
|`-i`|Ignore case|
|`-w`|Ignore whitespace|

### Practical use

Compare configuration before and after modification:

```
diff -u old.conf new.conf
```

Very useful when troubleshooting configuration changes.