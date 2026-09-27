
---
Tests IP connectivity using ICMP Echo Request/Reply.

### Syntax

```
ping [OPTIONS] DESTINATION
```

### Important options

|Option|Purpose|
|---|---|
|`-c N`|Send N packets|
|`-i N`|Interval between packets|
|`-W N`|Timeout|
|`-4`|IPv4|
|`-6`|IPv6|
|`-s N`|Packet size|

### Examples

```
ping 8.8.8.8
```

Send 4 packets:

```
ping -c 4 8.8.8.8
```

Test hostname resolution + connectivity:

```
ping -c 4 google.com
```

IPv4:

```
ping -4 -c 4 google.com
```

IPv6:

```
ping -6 -c 4 google.com
```

### Important

A failed `ping` does **not necessarily mean the host is unreachable**.

ICMP may simply be filtered.