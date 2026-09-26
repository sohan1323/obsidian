
---
Displays sessions connected to a computer's shared resources.

### Syntax

```
net session
```

Example:

```
net session
```

Can show information about remote clients connected to the local computer.

### `/delete`

Terminates a session:

```
net session \\CLIENT01 /delete
```

Use carefully because this disconnects the remote session.

Administrative privileges are generally required.