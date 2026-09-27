
---
Forwards a local port through SSH to a destination reachable from the remote SSH server.

### Syntax

```
ssh -L LOCAL_PORT:DEST_HOST:DEST_PORT USER@SSH_SERVER
```

Example:

```
ssh -L 8080:127.0.0.1:80 user@192.168.1.10
```

Conceptually:

```
Your machine
     |
localhost:8080
     |
    SSH
     |
192.168.1.10
     |
127.0.0.1:80
```

Now accessing:

```
curl http://127.0.0.1:8080
```

can reach the remote server's port 80 through the SSH tunnel.