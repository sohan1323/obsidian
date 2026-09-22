
---
Displays and manages network interfaces.

```
ip link
```

Short form:

```
ip l
```

Show one interface:

```
ip link show eth0
```

Bring interface up:

```
sudo ip link set eth0 up
```

Bring interface down:

```
sudo ip link set eth0 down
```

Show MAC address:

```
ip link show eth0
```

Change MTU:

```
sudo ip link set eth0 mtu 1400
```

### Practical use

Check whether an interface is:

```
UP
DOWN
```