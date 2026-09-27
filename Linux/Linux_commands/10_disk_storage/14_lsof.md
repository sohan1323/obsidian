
---
Lists **open files**.

Linux treats many resources as files, so `lsof` can show:

- processes
- files
- sockets
- devices
- network connections

### Syntax

```
lsof [OPTION]
```

### Examples

Find processes using a directory:

```
sudo lsof /var
```

Find a process using a specific file:

```
sudo lsof /var/log/auth.log
```

Find processes using a mount point:

```
sudo lsof /mnt
```

Find network-related open files:

```
sudo lsof -i
```

Find TCP connections:

```
sudo lsof -iTCP
```

Find a specific port:

```
sudo lsof -i :22
```

### Practical use

If you cannot unmount:

```
sudo lsof /mnt
```

If port `8080` is already occupied:

```
sudo lsof -i :8080
```