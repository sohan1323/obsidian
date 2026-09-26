
---
Deletes a service registration.

### Syntax

```
sc delete ServiceName
```

Example:

```
sc delete TestService
```

Usually stop it first:

```
sc stop TestService
sc delete TestService
```

**Important:** `sc delete` removes the service registration; it does not necessarily delete the executable referenced by the service.