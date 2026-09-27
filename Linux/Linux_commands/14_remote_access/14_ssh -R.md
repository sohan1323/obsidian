
---
Creates a listening port on the remote SSH side that forwards through the SSH connection.

### Syntax

```
ssh -R REMOTE_PORT:DEST_HOST:DEST_PORT USER@SSH_SERVER
```

Example:

```
ssh -R 9000:127.0.0.1:8080 user@192.168.1.10
```

Conceptually:

```
Remote server
     |
port 9000
     |
    SSH
     |
Your machine
     |
127.0.0.1:8080
```