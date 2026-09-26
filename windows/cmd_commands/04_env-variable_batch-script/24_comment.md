
---
Another commonly used batch-file comment syntax:

```
:: This is a comment
```

Example:

```
@echo off

:: Display username
echo %USERNAME%
```

For maximum compatibility in complex batch constructs, `rem` is generally safer than relying on `::` in every possible context.