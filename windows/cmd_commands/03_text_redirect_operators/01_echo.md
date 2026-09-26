
---
We already introduced `echo`, but it is important for text processing.

### Syntax

```
echo [message]
```

### Print text

```
echo Hello World
```

Output:

```
Hello World
```

### Print variable

```
echo %USERNAME%
```

### Print multiple variables

```
echo User=%USERNAME% Computer=%COMPUTERNAME%
```

Example:

```
User=Sohan Computer=DESKTOP-ABC123
```

### Write text to a file

```
echo Hello > test.txt
```

Creates/overwrites `test.txt`.

### Append text

```
echo Second line >> test.txt
```

Now:

```
type test.txt
```

produces:

```
Hello
Second line
```