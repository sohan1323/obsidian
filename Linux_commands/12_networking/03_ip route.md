
---
Displays and manages the routing table.

### Syntax

```
ip route [COMMAND]
```

Display routes:

```
ip route
```

Example:

```
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link
```

The important parts are:

```
default
    ↓
default gateway

192.168.1.0/24
    ↓
local network
```

Add a route:

```
sudo ip route add 10.10.10.0/24 via 192.168.1.1
```

Delete a route:

```
sudo ip route del 10.10.10.0/24
```

Check route to a specific destination:

```
ip route get 8.8.8.8
```

### Practical use

Determine where traffic will go:

```
ip route get 10.10.10.5
```