
---
Determines the sequence of network hops toward a destination.

```
traceroute -n 8.8.8.8
```

`-n` prevents reverse DNS lookups, making output faster and avoiding DNS-related confusion.

### TCP traceroute

Some networks block ICMP/UDP probes.

You can use TCP:

```
sudo traceroute -T -p 443 example.com
```

### UDP traceroute

```
traceroute -U example.com
```