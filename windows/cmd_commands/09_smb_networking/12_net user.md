
---
`net user` can query accounts on another computer.

### Syntax

```
net user /domain
```

Domain users:

```
net user /domain
```

Remote computer:

```
net user USERNAME /domain
```

For local accounts on another system, depending on permissions:

```
net user USERNAME \\SERVER01
```

The exact availability depends on Windows configuration and permissions.