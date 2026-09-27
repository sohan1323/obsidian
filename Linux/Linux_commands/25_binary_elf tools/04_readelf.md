
---
One of the most important ELF-analysis tools.

Used to inspect the internal structure of ELF files.

### Syntax

```
readelf [OPTIONS] FILE
```

---

## ELF Header

```
readelf -h ./program
```

Shows:

```
Class
Data encoding
Machine architecture
Entry point
Program header offset
Section header offset
Number of sections
```

Example:

```
Class: ELF64
Machine: Advanced Micro Devices X86-64
Entry point address: 0x401000
```

---

## Program Headers

```
readelf -l ./program
```

Shows segments loaded into memory.

More detail:

```
readelf -lW ./program
```

Important information:

```
LOAD
INTERP
DYNAMIC
GNU_STACK
GNU_RELRO
```

---

## Section Headers

```
readelf -S ./program
```

More readable for wide output:

```
readelf -SW ./program
```

Useful sections:

```
.text
.rodata
.data
.bss
.symtab
.strtab
.plt
.got
```

---

## Symbols

```
readelf -s ./program
```

Wide output:

```
readelf -sW ./program
```

Useful for identifying:

```
functions
global variables
undefined symbols
library references
```

---

## Dynamic Section

```
readelf -d ./program
```

Shows dynamic linking information.

For example:

```
NEEDED
RPATH
RUNPATH
```

---

## Dynamic Symbols

```
readelf --dyn-syms ./program
```

---

## Relocations

```
readelf -r ./program
```

Useful when studying:

```
dynamic linking
GOT
PLT
symbol resolution
```

---

## String / Note Sections

```
readelf -p .rodata ./program
```

---

## ELF Interpreter

```
readelf -l ./program | grep interpreter
```

Example:

```
[Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]
```