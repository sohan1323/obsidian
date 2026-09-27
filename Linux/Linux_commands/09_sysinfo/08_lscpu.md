
---
Displays detailed CPU architecture and processor information.

### Syntax

```
lscpu [OPTION]
```

### Examples

```
lscpu
```

Important information includes:

- CPU architecture
- CPU(s)
- cores
- threads
- sockets
- vendor
- model
- virtualization support
- CPU frequency information

Get specific information:

```
lscpu | grep 'CPU(s)'
```

```
lscpu | grep -i virtualization
```

### Practical use

CPU enumeration:

```
lscpu
```

Check virtualization support:

```
lscpu | grep -i virtualization
```