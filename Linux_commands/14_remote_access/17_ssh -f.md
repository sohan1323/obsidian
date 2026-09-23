
---
Moves SSH into the background after authentication.

Example:

```
ssh -f -N -L 8080:127.0.0.1:80 user@192.168.1.10
```

Useful for persistent tunnels.