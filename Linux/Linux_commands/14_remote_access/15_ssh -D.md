
---
Creates a SOCKS proxy through SSH.

### Syntax

```
ssh -D LOCAL_PORT USER@SSH_SERVER
```

Example:

```
ssh -D 1080 user@192.168.1.10
```

Applications configured to use:

```
SOCKS5
127.0.0.1:1080
```

can send traffic through the SSH connection.

### Practical security/lab use

Useful in authorized lab environments for accessing resources through an SSH-accessible pivot point.