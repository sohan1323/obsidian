
---
Syntax:

```
if "%var%"=="value" command
```

Example:

```
set "user=Sohan"

if "%user%"=="Sohan" (
    echo Correct user.
)
```

### `EQU`, `NEQ`, `LSS`, `LEQ`, `GTR`, `GEQ`

These are primarily numeric comparisons.

```
set /a age=20

if %age% GEQ 18 (
    echo Adult
)
```

Operators:

|Operator|Meaning|
|---|---|
|`EQU`|equal|
|`NEQ`|not equal|
|`LSS`|less than|
|`LEQ`|less than/equal|
|`GTR`|greater than|
|`GEQ`|greater than/equal|

Example:

```
set /a score=75

if %score% GEQ 50 (
    echo Pass
) else (
    echo Fail
)
```


# Case-Insensitive String Comparison

```
if /i "%choice%"=="yes" echo Yes selected
```

`/i` makes the comparison case-insensitive.

Therefore:

```
YES
Yes
yes
YeS
```

all match.