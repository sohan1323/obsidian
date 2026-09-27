
---
Combines functionality similar to:

```
ping + traceroute
```

and continuously monitors the path.

### Syntax

```
mtr [OPTIONS] HOST
```

### Examples

```
mtr google.com
```

Numeric mode:

```
mtr -n google.com
```

Report mode:

```
mtr -r -c 10 google.com
```

Here:

- `-r` = report mode
- `-c 10` = send 10 cycles

### Practical use

Identify packet loss or latency along the route:

```
mtr -rw -c 20 8.8.8.8
```