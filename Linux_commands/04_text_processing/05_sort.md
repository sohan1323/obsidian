
---
**Purpose:** Sort lines.

### Syntax

```
sort [OPTIONS] [FILE]
```

### Important options

|Option|Meaning|
|---|---|
|`-r`|Reverse|
|`-n`|Numeric sort|
|`-h`|Human-readable numeric sort|
|`-f`|Ignore case|
|`-u`|Remove duplicate lines|
|`-k FIELD`|Sort by field|
|`-t CHAR`|Specify field separator|
|`-o FILE`|Write output to file|

### Examples

Alphabetical:

```
sort names.txt
```

Reverse:

```
sort -r names.txt
```

Numeric:

```
sort -n numbers.txt
```

Unique:

```
sort -u names.txt
```

Sort `/etc/passwd` by UID:

```
sort -t ':' -k 3 -n /etc/passwd
```

Sort by username:

```
sort -t ':' -k 1 /etc/passwd
```

### Practical use

Find most common IPs:

```
cut -d ' ' -f 1 access.log | sort | uniq -c | sort -nr
```

This is a very useful Linux log-analysis pattern.