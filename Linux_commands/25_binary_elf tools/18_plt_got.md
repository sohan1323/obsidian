
---
Two important ELF concepts when studying dynamically linked programs.

### PLT

**Procedure Linkage Table**

Used to call dynamically linked functions.

Example:

```
printf@plt
puts@plt
malloc@plt
```

Inspect:

```
objdump -d -M intel ./program | grep plt
```

---

### GOT

**Global Offset Table**

Contains addresses used for dynamically resolved symbols.

Inspect:

```
objdump -R ./program
```

or:

```
readelf -r ./program
```

---

