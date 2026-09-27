
---
**Purpose:** Create an empty file or update a file's timestamps.

### Syntax

```
touch [OPTION]... FILE...
```

### Important options

|Option|Meaning|
|---|---|
|`-a`|Change access time only|
|`-m`|Change modification time only|
|`-c`|Do not create file if it doesn't exist|
|`-d DATE`|Use specified date/time|
|`-r FILE`|Copy timestamps from another file|

### Examples

Create a file:

```bash
touch file.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

Create a file inside another directory:

```
touch /tmp/test.txt
```

Update modification time:

```
touch file.txt
```

Don't create the file if it doesn't exist:

```
touch -c file.txt
```

Copy timestamps from another file:

```
touch -r original.txt copy.txt
```