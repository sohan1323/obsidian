
---
Compresses files using the **bzip2** algorithm.

### Syntax

```
bzip2 [OPTION] FILE
```

### Important options

|Option|Purpose|
|---|---|
|`-d`|Decompress|
|`-k`|Keep original|
|`-v`|Verbose|
|`-1` to `-9`|Compression level|

### Examples

```
bzip2 file.txt
```

Produces:

```
file.txt.bz2
```

Decompress:

```
bzip2 -d file.txt.bz2
```

Keep original:

```
bzip2 -k file.txt
```