
---
### Case 1

```
IP address:       ✓
Gateway ping:     ✓
8.8.8.8 ping:     ✓
example.com:      ✗
```

Likely area:

```
DNS resolution
```

Check:

```
resolvectl status
dig example.com
```

---

### Case 2

```
IP address:       ✓
Gateway ping:     ✗
```

Likely area:

```
local network/interface/routing/VLAN
```

Check:

```
ip link
ip addr
ip route
ip neigh
```

---

### Case 3

```
8.8.8.8:          ✓
TCP 443:          ✓
ping example.com: ✗
```

Do not immediately conclude the host is unreachable.

ICMP may be blocked.

Test:

```
curl -I https://example.com
```