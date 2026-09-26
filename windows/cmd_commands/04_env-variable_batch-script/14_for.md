
---
`for` performs repeated operations.

### Basic syntax

```
for %variable in (set) do command
```

At an interactive CMD prompt, use:

```
for %f in (*.txt) do echo %f
```

Inside a `.bat` file, you must use **double percent signs**:

```
for %%f in (*.txt) do echo %%f
```

This distinction is extremely important.

---

## Example

```
for %f in (*.txt) do echo %f
```

If the directory contains:

```
a.txt
b.txt
c.txt
```

you get:

```
a.txt
b.txt
c.txt
```