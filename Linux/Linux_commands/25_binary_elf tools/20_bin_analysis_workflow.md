
---
For an unknown ELF binary:

### Step 1 — Identify

```
file ./program
```

### Step 2 — ELF header

```
readelf -h ./program
```

### Step 3 — Sections

```
readelf -SW ./program
```

### Step 4 — Program segments

```
readelf -lW ./program
```

### Step 5 — Dependencies

```
readelf -d ./program
```

### Step 6 — Symbols

```
nm ./program
```

or:

```
readelf -sW ./program
```

### Step 7 — Strings

```
strings ./program
```

### Step 8 — Disassembly

```
objdump -d -M intel ./program
```

### Step 9 — Security protections

```
checksec --file=./program
```

### Step 10 — Libraries

```
ldd ./program
```