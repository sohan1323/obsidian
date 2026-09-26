
---
Save output:

```
systeminfo > systeminfo.txt
```

Append:

```
systeminfo >> systeminfo.txt
```

Suppress output:

```
command >nul
```

Suppress errors:

```
command 2>nul
```

Both:

```
command >output.txt 2>&1
```

Example:

```
ipconfig /all > "%~dp0network.txt" 2>&1
```