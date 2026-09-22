
---
**Purpose:** Remove or count **consecutive duplicate lines**.

### Syntax

```
uniq [OPTIONS] [INPUT [OUTPUT]]
```

### Important options

|Option|Meaning|
|---|---|
|`-c`|Count occurrences|
|`-d`|Show only duplicates|
|`-u`|Show only unique lines|
|`-i`|Ignore case|
|`-f N`|Ignore first N fields|

### Examples

```
uniq names.txt
```

Count duplicates:

```
uniq -c names.txt
```

Show only duplicates:

```
uniq -d names.txt
```

### Important concept

`uniq` works on **adjacent duplicate lines**.

Therefore:

```
uniq names.txt
```

doesn't necessarily find all duplicates.

Usually use:

```
sort names.txt | uniq
```

or simply:

```
sort -u names.txt
```

### Very useful pattern

```
sort access.log | uniq -c | sort -nr
```

This gives frequency counts sorted from highest to lowest.