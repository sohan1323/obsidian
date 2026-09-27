
---
Removes a host from the local `known_hosts` file.

```
ssh-keygen -R 192.168.1.10
```

Useful when a legitimate server's host key has changed, for example after rebuilding a lab VM.