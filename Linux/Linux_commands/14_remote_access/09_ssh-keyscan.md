
---
Retrieves SSH public host keys from remote servers.

### Syntax

```
ssh-keyscan [OPTIONS] HOST
```

### Examples

```
ssh-keyscan 192.168.1.10
```

Specific port:

```
ssh-keyscan -p 2222 192.168.1.10
```

IPv4:

```
ssh-keyscan -4 192.168.1.10
```

Save output:

```
ssh-keyscan 192.168.1.10 > host_keys.txt
```

### Practical use

Collect SSH host-key information from systems you are authorized to assess.