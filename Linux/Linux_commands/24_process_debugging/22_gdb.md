
---
GNU Debugger is used for debugging programs.

Start:

```
gdb ./program
```

Inside GDB:

```
run
break
continue
next
step
print
backtrace
quit
```

Example:

```
gdb ./program
```

Then:

```
(gdb) break main
(gdb) run
(gdb) next
(gdb) print variable
(gdb) backtrace
```


# `gdb` — Attach to Process

Attach:

```
gdb -p PID
```

This allows debugging a running process if permissions and system security settings permit it.


# `gdb` Core Commands

### Start program

```
run
```

### Set breakpoint

```
break main
```

or:

```
break function_name
```

### Continue

```
continue
```

### Step over

```
next
```

### Step into

```
step
```

### Show call stack

```
backtrace
```

### Inspect variable

```
print variable
```

### Exit

```
quit
```


