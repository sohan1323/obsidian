
---
Older interactive TCP client.

It is **not secure** for normal remote login because traffic is unencrypted.

It can still be useful for basic TCP connectivity testing.

### Syntax

```
telnet HOST PORT
```

Example:

```
telnet 192.168.1.10 80
```

For modern systems, `nc` is generally more useful:

```
nc -vz 192.168.1.10 80
```