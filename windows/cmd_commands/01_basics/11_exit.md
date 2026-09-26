
---
Closes the current CMD session or exits a batch script.

### Syntax

```
exit [/b] [exitCode]
```

### Arguments

|Argument|Meaning|
|---|---|
|`/b`|Exit the current batch script instead of terminating CMD|
|`exitCode`|Numeric exit status|

### Examples

Exit CMD:

```
exit
```

Exit a batch script:

```
exit /b
```

Return an exit code:

```
exit /b 0
```

Return an error:

```
exit /b 1
```

### Why exit codes matter

Windows programs commonly use:

```
0     = success
non-0 = error/failure
```

You can inspect the previous command's exit code with:

```
echo %ERRORLEVEL%
```

Example:

```
dir C:\DoesNotExist
echo %ERRORLEVEL%
```