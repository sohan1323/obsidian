
---
Displays sizes of sections in an object/executable.

### Syntax

```
size FILE
```

Example:

```
size ./program
```

Typical output:

```
   text   data    bss    dec    hex
   5420    720    320   6460   193c
```

Meaning:

| Field  | Meaning            |
| ------ | ------------------ |
| `text` | Code               |
| `data` | Initialized data   |
| `bss`  | Uninitialized data |
| `dec`  | Decimal total      |
| `hex`  | Hexadecimal total  |