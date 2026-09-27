
---
Queries the system DNS resolver.

### Syntax

```
resolvectl [COMMAND]
```

### Examples

Show DNS configuration:

```
resolvectl status
```

Resolve a hostname:

```
resolvectl query example.com
```

Show DNS servers:

```
resolvectl dns
```

### Practical use

DNS troubleshooting:

```
resolvectl status
```