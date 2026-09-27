
---
Shows the network hops between your system and a destination.

### Syntax

```
traceroute [OPTIONS] HOST
```

### Examples

```
traceroute google.com
```

IPv4:

```
traceroute -4 google.com
```

Numeric output without DNS resolution:

```
traceroute -n google.com
```

Specify maximum hops:

```
traceroute -m 20 google.com
```

### Practical use

Identify where packets stop:

```
traceroute -n 8.8.8.8
```