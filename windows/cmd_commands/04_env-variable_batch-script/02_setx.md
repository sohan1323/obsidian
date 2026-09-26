
---
`setx` creates **persistent environment variables**.

### Important difference

```
set
```

changes the environment of the **current CMD process**.

```
setx
```

writes the variable persistently so that **future processes** can see it.

### Syntax

```
setx variable value
```

### Example

```
setx MYAPP "C:\MyApplication"
```

A newly opened CMD can then use:

```
echo %MYAPP%
```

### `/M`

Creates a system-wide environment variable instead of a user variable.

```
setx MYAPP "C:\MyApplication" /M
```

This generally requires an elevated CMD.

### Important

Don't use `setx` repeatedly to modify `PATH` casually. It can cause undesirable PATH changes, and it does not modify the environment of the already-running CMD process.