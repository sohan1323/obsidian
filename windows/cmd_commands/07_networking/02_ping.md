
---
Tests IP connectivity using ICMP Echo Request/Reply.

### Syntax

```
ping [-t] [-a] [-n count] [-l size] [-f] [-i TTL] [-w timeout]
     [-r count] [-s count] [-4] [-6] target
```

---

## Basic

```
ping 8.8.8.8
```

Tests connectivity to the target.

Hostname:

```
ping google.com
```

This tests both:

1. DNS resolution
2. ICMP connectivity

---

## `-t`

Continuous ping:

```
ping -t 8.8.8.8
```

Stop with:

```
Ctrl+C
```

---

## `-n`

Number of requests:

```
ping -n 5 8.8.8.8
```

Sends five packets.

---

## `-l`

Packet size:

```
ping -l 1000 8.8.8.8
```

Sends 1000-byte payloads.

---

## `-w`

Timeout in milliseconds:

```
ping -w 1000 8.8.8.8
```

Timeout = 1000 ms.

---

## `-a`

Resolve an IP address to a hostname where possible:

```
ping -a 192.168.1.1
```

---

## `-4`

Force IPv4:

```
ping -4 example.com
```

## `-6`

Force IPv6:

```
ping -6 example.com
```

---

## Important interpretation

If:

```
ping 8.8.8.8
```

works but:

```
ping google.com
```

doesn't, DNS may be involved.

If both fail, possible causes include:

- routing
- firewall
- network adapter
- gateway
- Internet connectivity
- target blocking ICMP

**Ping failure does not automatically mean the host is down.**