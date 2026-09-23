
---
Do not execute a remote shell/command.

Useful when SSH is being used only for port forwarding.

Example:

```
ssh -N -L 8080:127.0.0.1:80 user@192.168.1.10
```