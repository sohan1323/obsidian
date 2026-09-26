
---
Normally:

```
%variable%
```

is expanded when CMD parses a command block.

This can cause surprising behavior.

Consider:

```
@echo off

set count=0

for %%i in (1 2 3) do (
    set /a count+=1
    echo %count%
)
```

You might expect:

```
1
2
3
```

but `%count%` can be expanded before the block executes.

---

## Enable delayed expansion

```
setlocal EnableDelayedExpansion
```

Then use:

```
!count!
```

Example:

```
@echo off

setlocal EnableDelayedExpansion

set count=0

for %%i in (1 2 3) do (
    set /a count+=1
    echo !count!
)

endlocal
```

Output:

```
1
2
3
```

This distinction is critical:

```
%variable%
```

= normal expansion

```
!variable!
```

= delayed expansion