
---
**Purpose:** Display a file **in reverse line order**.

`cat` → beginning to end.

`tac` → end to beginning.

### Syntax

```
tac [OPTION]... [FILE]...
```

### Examples

```
tac file.txt
```

If the file contains:

```
line 1
line 2
line 3
line 4
```

Output:

```
line 4
line 3
line 2
line 1
```

### Practical use

Useful when you want to inspect the **most recent entries first** in a line-oriented log:

```
tac logfile.txt
```