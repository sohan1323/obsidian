
---
`checksec` summarizes common binary security protections.

Check installation:

```
which checksec
```

Example:

```
checksec --file=./program
```

Typical protections:

```
RELRO
Stack Canary
NX
PIE
RPATH
RUNPATH
Symbols
```

---

## Important protections

### NX

Prevents execution from certain writable memory regions.

```
NX enabled
```

---

### PIE

Position Independent Executable.

```
PIE enabled
```

Allows the executable to be relocated in memory.

---

### Canary

Stack protection mechanism.

```
Canary found
```

---

### RELRO

Protects parts of ELF relocation structures.

Possible states:

```
No RELRO
Partial RELRO
Full RELRO
```

---

### Example

```
checksec --file=/bin/bash
```

This is particularly useful in CTF/binary-analysis environments.