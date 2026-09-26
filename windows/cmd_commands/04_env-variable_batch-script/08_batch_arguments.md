
---
Create:

```
hello.bat
```

with:

```
@echo off
echo First argument: %1
echo Second argument: %2
```

Run:

```
hello.bat Windows PowerShell
```

Output:

```
First argument: Windows
Second argument: PowerShell
```

The mapping is:

```
%0 → script name
%1 → first argument
%2 → second argument
%3 → third argument
...
%9 → ninth argument
```

Example:

```
backup.bat C:\Data D:\Backup
```

Inside:

```
%1 = C:\Data
%2 = D:\Backup
```