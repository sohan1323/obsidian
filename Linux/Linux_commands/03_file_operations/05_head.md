
---
**Purpose:** Display the beginning of a file.

### Syntax

```
head [OPTION]... [FILE]...
```

By default, it displays the first **10 lines**.

### Important options

|Option|Meaning|
|---|---|
|`-n NUMBER`|Show NUMBER lines|
|`-NUMBER`|Older shorthand for NUMBER lines|
|`-c NUMBER`|Show NUMBER bytes|
|`-q`|Don't print filenames|
|`-v`|Always print filenames|

### Examples

First 10 lines:

```
head file.txt
```

First 5 lines:

```
head -n 5 file.txt
```

First 20 lines:

```
head -n 20 file.txt
```

First 100 bytes:

```
head -c 100 file.txt
```

Multiple files:

```
head file1.txt file2.txt
```

### Practical use

Quickly inspect the beginning of a configuration or data file:

```
head /etc/passwd
```