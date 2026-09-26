
---
Sends a control code to a service.

### Syntax

```
sc control ServiceName ControlCode
```

Example:

```
sc control MyService 128
```

Service-specific control codes depend on the service.

This is an advanced operation and is not equivalent to simply stopping or starting a service.