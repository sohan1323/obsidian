
---
Displays/configures network interfaces.

It is an **older/deprecated-style tool** on many modern Linux systems.

Prefer:

```
ip addr
ip link
```

### Examples

```
ifconfig
```

Specific interface:

```
ifconfig eth0
```

Bring interface up:

```
sudo ifconfig eth0 up
```

Bring down:

```
sudo ifconfig eth0 down
```

### Important

For modern Linux administration, learn `ip` first.