
---
The user's SSH client configuration is commonly:

```
~/.ssh/config
```

Example:

```
Host lab-server
    HostName 192.168.1.10
    User kali
    Port 22
    IdentityFile ~/.ssh/id_ed25519
```

Then simply:

```
ssh lab-server
```

### Check effective configuration

```
ssh -G lab-server
```

This prints the configuration SSH would use.