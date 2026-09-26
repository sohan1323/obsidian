
---
Displays sessions connected to the local computer's shared resources.

```
net session
```

Example information can include:

```
Computer       User name       Client Type
------------------------------------------
\\192.168.1.50 alice
```

This can help an administrator determine which clients currently have SMB sessions.

---

## Delete a session

```
net session \\192.168.1.50 /delete
```

Delete all sessions:

```
net session /delete
```

Use carefully because this disconnects clients.