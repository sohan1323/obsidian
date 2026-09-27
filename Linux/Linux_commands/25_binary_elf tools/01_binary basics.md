
---
A binary file contains data represented as bytes rather than human-readable text.

Common Linux binary types:

```
Executable programs
Shared libraries (.so)
Object files (.o)
Static libraries (.a)
Core dumps
Firmware
```

Linux executables commonly use the **ELF — Executable and Linkable Format**.

Basic check:

```
file /bin/ls
```

Typical output:

```
/bin/ls: ELF 64-bit LSB pie executable, x86-64, ...
```