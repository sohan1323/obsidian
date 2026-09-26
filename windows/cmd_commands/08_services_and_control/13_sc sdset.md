
---
Changes a service's security descriptor.

### Syntax

```
sc sdset ServiceName SecurityDescriptor
```

Example:

```
sc sdset MyService <SDDL>
```

This is an advanced administrative operation.

Incorrect SDDL can lock administrators out of service-management operations, so use it only when you understand the descriptor being applied.