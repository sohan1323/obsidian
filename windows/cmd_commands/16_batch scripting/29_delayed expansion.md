
---
This is one of the most important advanced batch concepts.

Normally:

```
%variable%
```

is expanded when the entire parenthesized block is parsed.

Example:

```
@echo off

set count=0

for %%f in (*.txt) do (
    set /a count+=1
    echo Count: %count%
)
```

You can encounter unexpected results.

Use delayed expansion:

```
@echo off

setlocal EnableDelayedExpansion

set count=0

for %%f in (*.txt) do (
    set /a count+=1
    echo Count: !count!
)

endlocal
```

The key difference:

```
%count%  → normal expansion
!count!  → delayed expansion
```

Enable:

```
setlocal EnableDelayedExpansion
```

Disable:

```
setlocal DisableDelayedExpansion
```