
---
Determines exactly how Linux would route traffic to a destination.

```
ip route get 8.8.8.8
```

Example:

```
8.8.8.8 via 192.168.1.1 dev eth0 src 192.168.1.20
```

This tells you:

```
Destination → 8.8.8.8
Gateway     → 192.168.1.1
Interface   → eth0
Source IP   → 192.168.1.20
```

### Practical use

Very useful when troubleshooting multiple interfaces/VPNs:

```
ip route get 10.10.10.10
```