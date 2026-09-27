
---
`objdump` displays information from object files and executables.

### Syntax

```
objdump [OPTIONS] FILE
```

---

## Disassemble

```
objdump -d ./program
```

Disassemble executable sections.

For Intel syntax:

```
objdump -d -M intel ./program
```

This is commonly useful for reverse engineering.

---

## Disassemble All Sections

```
objdump -D ./program
```

Difference:

```
-d
    Disassemble executable sections

-D
    Disassemble all sections
```

---

## Headers

```
objdump -f ./program
```

---

## Section Headers

```
objdump -h ./program
```

---

## Symbols

```
objdump -t ./program
```

Dynamic symbols:

```
objdump -T ./program
```

---

## Private Headers

```
objdump -p ./program
```

Useful for inspecting:

```
dynamic section
interpreter
needed libraries
program information
```

---

## Example

```
objdump -d -M intel ./program | less
```