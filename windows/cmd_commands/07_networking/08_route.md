
---
Displays and modifies the IP routing table.

### Syntax

```
route print
route add
route delete
route change
```

---

## Display routing table

```
route print
```

You'll see routes such as:

```
Network Destination
Netmask
Gateway
Interface
Metric
```

---

## Display IPv4 routes

```
route print -4
```

## IPv6

```
route print -6
```

---

## Add a route

General form:

```
route add destination mask netmask gateway
```

Example:

```
route add 10.10.10.0 mask 255.255.255.0 192.168.1.1
```

This modifies the routing table.

---

## Persistent route

```
route -p add 10.10.10.0 mask 255.255.255.0 192.168.1.1
```

`-p` makes the route persistent across restarts.

---

## Delete route

```
route delete 10.10.10.0
```

Be careful when modifying routing tables on machines with active network connections.