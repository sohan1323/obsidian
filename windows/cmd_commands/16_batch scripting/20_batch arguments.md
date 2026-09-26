
---
Suppose:

```
backup.bat C:\Lab D:\Backup
```

Inside the script:

```
%0 = backup.bat
%1 = C:\Lab
%2 = D:\Backup
```

Example:

```
@echo off

echo Script: %0
echo Source: %1
echo Destination: %2
```



# `%*`

Represents all arguments.

```
@echo off

echo Arguments:
echo %*
```

Run:

```
test.bat one two three
```

Output:

```
Arguments:
one two three
```


# `%~1`

Removes surrounding quotes.

If:

```
script.bat "C:\My Files"
```

Then:

```
echo %1
```

may preserve:

```
"C:\My Files"
```

while:

```
echo %~1
```

produces:

```
C:\My Files
```