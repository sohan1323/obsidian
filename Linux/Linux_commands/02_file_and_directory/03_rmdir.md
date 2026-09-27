
---
**Purpose:** Remove **empty directories**.

### Syntax

```
rmdir [OPTION]... DIRECTORY...
```

### Important options

|Option|Meaning|
|---|---|
|`-p`|Remove parent directories if they become empty|
|`-v`|Verbose output|

### Examples

```
mkdir test
rmdir test
```

Remove multiple empty directories:

```
rmdir dir1 dir2 dir3
```

Remove nested empty directories:

```
rmdir -p project/src/python
```

### Important

`rmdir` will **not remove a directory containing files**.

For example:

```
rmdir documents
```

may return:

```
Directory not empty
```

For non-empty directories, `rm -r` is used.