
---
**Purpose:** Compare files byte-by-byte.

### Syntax

```
cmp [OPTIONS] FILE1 FILE2
```

### Examples

```
cmp file1.bin file2.bin
```

If identical, normally no output.

Show the first difference:

```
cmp -l file1.bin file2.bin
```

### `diff` vs `cmp`

| Command | Use                             |
| ------- | ------------------------------- |
| `diff`  | Human-readable text differences |
| `cmp`   | Byte-level comparison           |