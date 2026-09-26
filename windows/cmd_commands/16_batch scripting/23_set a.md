
---
Performs arithmetic.

```
set /a x=10+5
echo %x%
```

Output:

```
15
```

Operators include:

```
+
-
*
/
%
```

Example:

```
set /a result=20*5
echo %result%
```

Increment:

```
set /a count+=1
```

Decrement:

```
set /a count-=1
```

Multiple expressions:

```
set /a a=10, b=20, c=a+b
echo %c%
```