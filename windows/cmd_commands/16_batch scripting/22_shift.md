
---
Moves command-line arguments.

Example:

```
@echo off

echo First: %1

shift

echo New first: %1
```

Run:

```
script.bat A B C
```

Initially:

```
%1 = A
%2 = B
%3 = C
```

After:

```
shift
```

they become:

```
%1 = B
%2 = C
```

Useful when processing an arbitrary number of arguments.