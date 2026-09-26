
---
## `set`

Syntax:

```
set VARIABLE=value
```

Example:

```
set name=Sohan
echo %name%
```

Output:

```
Sohan
```

### Numeric variable

```
set count=10
echo %count%
```

### Spaces matter

Correct:

```
set name=Sohan
```

Avoid:

```
set name = Sohan
```

The latter can create a variable named `name` with a trailing space.

### Safer syntax

```
set "name=Sohan"
```

This is recommended because it prevents accidental trailing spaces.

```
set "path=C:\Lab Files"
```