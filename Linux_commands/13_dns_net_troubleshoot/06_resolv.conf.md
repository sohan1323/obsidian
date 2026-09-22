
---
Contains DNS resolver configuration on many Linux systems.

View it:

```
cat /etc/resolv.conf
```

Typical entry:

```
nameserver 192.168.1.1
```

Multiple servers can exist:

```
nameserver 192.168.1.1
nameserver 8.8.8.8
```

### Practical use

Check which resolver configuration the system is using.

```
cat /etc/resolv.conf
```

On some distributions, this file is managed automatically and may be a symbolic link.