
---
`set` can also perform arithmetic.

### Syntax

```
set /a expression
```

Example:

```
set /a 5+5
```

Output:

```
10
```

Assign result:

```
set /a total=5+5
echo %total%
```

Output:

```
10
```

Increment:

```
set /a count+=1
```

Decrement:

```
set /a count-=1
```

Multiply:

```
set /a result=10*5
```

Divide:

```
set /a result=20/4
```

Modulo:

```
set /a result=10%%3
```

In a batch file, `%` has special meaning, so modulo often requires `%%`.