
---
Displays or modifies the executable search PATH.

### Display PATH

```
path
```

or:

```
echo %PATH%
```

### Set PATH for current CMD

```
path C:\Tools;C:\Python312;%PATH%
```

Now CMD searches these directories when locating executables.

### Example

Suppose:

```
C:\Tools\mytool.exe
```

exists.

You could temporarily add:

```
path C:\Tools;%PATH%
```

Then:

```
mytool
```

can locate the executable.

### Why PATH matters

When you execute:

```
python
```

CMD searches directories listed in `%PATH%` to locate an executable such as:

```
python.exe
```

You can investigate the resolution with:

```
where python
```