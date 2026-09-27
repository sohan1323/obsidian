
---
Compresses individual files using the **gzip** algorithm.

### Syntax

```
gzip [OPTION] FILE
```

### Important options

|Option|Purpose|
|---|---|
|`-d`|Decompress|
|`-k`|Keep original|
|`-c`|Write output to stdout|
|`-1`|Fastest compression|
|`-9`|Highest compression|
|`-v`|Verbose|
|`-r`|Recursively compress|

### Examples

Compress:

```
gzip file.txt
```

This produces:

```
file.txt.gz
```

Decompress:

```
gzip -d file.txt.gz
```

Keep original:

```
gzip -k file.txt
```

Maximum compression:

```
gzip -9 file.txt
```

Decompress while keeping the `.gz` file:

```
gzip -dk file.txt.gz
```