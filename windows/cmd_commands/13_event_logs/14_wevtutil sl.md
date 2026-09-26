
---
`sl` = **Set Log configuration**

Example:

```
wevtutil sl System
```

Specific options can configure:

- Enabled state
- Maximum size
- Retention
- Log file

Because incorrect settings can affect logging, inspect first:

```
wevtutil gl System
```