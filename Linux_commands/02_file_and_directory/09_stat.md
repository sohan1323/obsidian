
---
**Purpose:** Display detailed file/directory metadata.

### Syntax

```
stat [OPTION] FILE...
```

### Examples

```
stat file.txt
```

Typical information includes:

```
File
Size
Blocks
IO Block
Inode
Links
Access
Modify
Change
Birth
```

### Important options

|Option|Meaning|
|---|---|
|`-c FORMAT`|Custom output format|
|`-f`|Show filesystem information|
|`-L`|Follow symbolic links|
|`-t`|Terse output|

### Examples

Show inode:

```
stat -c '%i' file.txt
```

Show permissions:

```
stat -c '%A' file.txt
```

Show numeric permissions:

```
stat -c '%a' file.txt
```

Show owner:

```
stat -c '%U' file.txt
```

Show modification time:

```
stat -c '%y' file.txt
```