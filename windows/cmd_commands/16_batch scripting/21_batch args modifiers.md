
---
Very useful when manipulating paths.

Given:

```
%1 = C:\Lab\test.txt
```

|Modifier|Meaning|
|---|---|
|`%~1`|remove quotes|
|`%~f1`|full path|
|`%~d1`|drive|
|`%~p1`|path|
|`%~n1`|filename|
|`%~x1`|extension|
|`%~dp1`|drive + path|
|`%~nx1`|filename + extension|
|`%~dpnx1`|full path|

Example:

```
@echo off

echo Full: %~f1
echo Drive: %~d1
echo Path: %~p1
echo Name: %~n1
echo Extension: %~x1
```

Run:

```
script.bat "C:\Lab\report.txt"
```

# `%~dp0`

One of the most useful batch variables.

```
%~dp0
```

means:

**drive + path of the currently executing batch file.**

Suppose:

```
C:\Tools\script.bat
```

contains:

```
echo %~dp0
```

Output:

```
C:\Tools\
```

Useful for scripts that need to reference files relative to themselves.

Example:

```
copy "%~dp0config.txt" "C:\Lab\"
```