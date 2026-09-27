
---
Displays and manages Ethernet interface information.

### Syntax

```
sudo ethtool INTERFACE
```

### Examples

```
sudo ethtool eth0
```

Show interface statistics:

```
sudo ethtool -S eth0
```

Show driver information:

```
sudo ethtool -i eth0
```

Show supported features:

```
sudo ethtool -k eth0
```

### Practical use

Check:

- link status
- negotiated speed
- duplex
- driver
- hardware features