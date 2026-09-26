
---
Check whether a variable exists.

```
if defined VARIABLE command
```

Example:

```
set "NAME=Sohan"

if defined NAME (
    echo NAME is defined.
)
```

Negation:

```
if not defined NAME echo NAME is not defined.
```