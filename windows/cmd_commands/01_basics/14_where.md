
---
Finds the location of executable files.

### Syntax

```
where [options] name
```

### Important arguments

|Argument|Meaning|
|---|---|
|`/R path`|Search recursively|
|`/Q`|Quiet mode; only return exit status|
|`/F`|Display filenames in quotes|
|`/T`|Display file timestamp and size|

### Basic example

```
where notepad
```

Possible result:

```
C:\Windows\System32\notepad.exe
```

Find Python:

```
where python
```

Find Git:

```
where git
```

Find all matches:

```
where /R C:\ python.exe
```

### Why this is important

`where` is particularly useful for understanding **PATH resolution**.

For example:

```
where python
```

may return multiple installations:

```
C:\Python312\python.exe
C:\Users\Sohan\AppData\Local\Programs\Python\Python313\python.exe
```

This tells you which executable locations are discoverable through PATH.