
---
Combines concepts from `ping` and `tracert` and provides packet-loss/latency statistics across the route.

### Syntax

```
pathping [-n] [-h maximum_hops] [-g host-list] [-p period]
         [-q numqueries] [-w timeout] [-4] [-6] target
```

### Basic

```
pathping google.com
```

It first discovers the route and then performs repeated measurements.

---

## `-n`

Don't resolve addresses to hostnames.

```
pathping -n google.com
```

## `-h`

Maximum hops:

```
pathping -h 20 google.com
```

## `-q`

Number of queries per hop:

```
pathping -q 10 google.com
```

## `-w`

Timeout:

```
pathping -w 1000 google.com
```

`pathping` can take significantly longer than `ping` or `tracert`.