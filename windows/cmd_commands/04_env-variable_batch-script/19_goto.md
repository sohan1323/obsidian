
---
Jumps to a label in a batch file.

Example:

```
@echo off

goto start

echo This won't execute

:start
echo Script started
```

Labels begin with:

```
:label
```

Example:

```
goto menu
```

jumps to:

```
:menu
```