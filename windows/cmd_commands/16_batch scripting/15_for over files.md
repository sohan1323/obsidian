
---
```
for %%f in (*.txt) do echo %%f
```

Example:

```
@echo off

for %%f in ("C:\Lab\*.txt") do (
    echo File: %%f
)
```


# `for /d`

Processes directories.

```
for /d %%d in (C:\Lab\*) do echo %%d
```

Example:

```
@echo off

for /d %%d in ("C:\Users\*") do (
    echo Directory: %%d
)
```


# `for /r`

Recursive file search.

Syntax:

```
for /r "directory" %%f in (pattern) do command
```

Example:

```
for /r "C:\Lab" %%f in (*.txt) do echo %%f
```

This searches subdirectories recursively.

Useful for:

- finding files
- processing logs
- automation
- authorized security-lab enumeration

Example:

```
for /r "C:\Lab" %%f in (*.log) do (
    echo Processing %%f
)
```


# `for /l`

Numeric loop.

Syntax:

```
for /l %%variable in (start,step,end) do command
```

Example:

```
for /l %%i in (1,1,5) do echo %%i
```

Output:

```
1
2
3
4
5
```

Count by 2:

```
for /l %%i in (0,2,10) do echo %%i
```

Output:

```
0
2
4
6
8
10
```

Countdown:

```
for /l %%i in (10,-1,1) do echo %%i
```


# `for /f`

`for /f` parses:

- text files
- command output
- strings

Example:

```
for /f "delims=" %%i in (file.txt) do echo %%i
```

Process command output:

```
for /f "delims=" %%i in ('hostname') do echo %%i
```

Another example:

```
for /f "delims=" %%i in ('whoami') do (
    echo Current user: %%i
)
```

This is extremely useful for automation.


# `for /f` — `delims`

Suppose:

```
Alice:Administrator
Bob:Users
```

Use:

```
for /f "tokens=1 delims=:" %%a in (users.txt) do echo %%a
```

Output:

```
Alice
Bob
```

`delims=:` tells `for /f` to split fields at `:`.


# `tokens`

Example:

```
Alice Administrator
Bob Users
```

Command:

```
for /f "tokens=1,2" %%a in (users.txt) do echo %%a %%b
```

Output:

```
Alice Administrator
Bob Users
```

Multiple variables:

```
tokens=1,2,3
```

gives:

```
%%a
%%b
%%c
```

# `tokens=*`

```
for /f "tokens=*" %%a in (file.txt) do echo %%a
```

Useful for reading lines while removing leading delimiters/spaces according to `for /f` parsing behavior.

# `skip`

Skip the first N lines.

```
for /f "skip=1" %%a in (file.txt) do echo %%a
```

Skip first 3:

```
for /f "skip=3" %%a in (file.txt) do echo %%a
```

Useful for processing files with headers.


# `eol`

Defines a character that marks a comment line for `for /f`.

```
for /f "eol=#" %%a in (config.txt) do echo %%a
```

Lines beginning with `#` are ignored.


# `usebackq`

Useful when working with quoted filenames and command strings.

Example:

```
for /f "usebackq delims=" %%a in ("C:\Lab\my file.txt") do echo %%a
```

It is particularly useful when filenames contain spaces.