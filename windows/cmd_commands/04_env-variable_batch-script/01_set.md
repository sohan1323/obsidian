
---
`set` displays, creates, modifies, and removes environment variables.

### Syntax

```
set [variable=[string]]
```

### Display all variables

```
set
```

You'll see variables such as:

```
USERNAME=Sohan
USERPROFILE=C:\Users\Sohan
TEMP=C:\Users\Sohan\AppData\Local\Temp
PATH=...
```

### Display one variable

```
set PATH
```

This displays variables beginning with `PATH`.

### Create variable

```
set name=Sohan
```

Check:

```
echo %name%
```

Output:

```
Sohan
```

---

## Variables containing spaces

You don't need quotes:

```
set name=John Smith
```

Then:

```
echo %name%
```

Output:

```
John Smith
```

Avoid:

```
set name = John
```

because spaces become part of the variable name/value.

---

## Delete variable

```
set name=
```

Now:

```
echo %name%
```

will normally show:

```
%name%
```

because the variable no longer exists.