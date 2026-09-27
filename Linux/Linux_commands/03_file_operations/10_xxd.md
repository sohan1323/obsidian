
---
**Purpose:** Create a hexadecimal dump or convert hexadecimal data back into binary.

### Syntax

```
xxd [OPTION] [FILE]
```

### Important options

|Option|Meaning|
|---|---|
|`-l LENGTH`|Limit number of bytes|
|`-s OFFSET`|Start at offset|
|`-c COLUMNS`|Bytes per line|
|`-g BYTES`|Group bytes|
|`-r`|Reverse hex dump → binary|
|`-p`|Plain hexadecimal output|

### Examples

Hex dump:

```
xxd file.bin
```

Limit output:

```
xxd -l 64 file.bin
```

Start at offset:

```
xxd -s 100 file.bin
```

Plain hexadecimal:

```
xxd -p file.bin
```

### Reverse a hex dump

Suppose:

```
48656c6c6f
```

represents:

```
Hello
```

You can convert hexadecimal back to binary data:

```
echo "48656c6c6f" | xxd -r -p
```

Output:

```
Hello
```

### Practical cybersecurity use

`xxd` is useful when examining:

- Binary files
- File headers/magic bytes
- Network data
- Encoded data
- Shellcode
- Exploit development

For example:

```
xxd -l 16 suspicious_file
```

lets you inspect the first 16 bytes.