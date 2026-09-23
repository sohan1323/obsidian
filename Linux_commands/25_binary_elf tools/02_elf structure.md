
---
An ELF file broadly contains:

```
ELF Header
    ↓
Program Headers
    ↓
Sections
    ├── .text
    ├── .data
    ├── .rodata
    ├── .bss
    ├── .symtab
    ├── .strtab
    ├── .plt
    ├── .got
    └── ...
```

Important concepts:

| Component       | Purpose                               |
| --------------- | ------------------------------------- |
| ELF Header      | Basic information about the binary    |
| Program Headers | Describe segments loaded into memory  |
| Section Headers | Describe sections used during linking |
| `.text`         | Executable machine code               |
| `.data`         | Initialized writable data             |
| `.rodata`       | Read-only data                        |
| `.bss`          | Uninitialized global/static data      |
| `.symtab`       | Symbol table                          |
| `.strtab`       | String table                          |
| `.plt`          | Procedure Linkage Table               |
| `.got`          | Global Offset Table                   |
| Interpreter     | Dynamic linker used by the binary     |