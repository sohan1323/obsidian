
---
Displays services that depend on a particular service.

### Syntax

```
sc enumdepend ServiceName
```

Example:

```
sc enumdepend RpcSs
```

This is useful before stopping a service because other services may depend on it.