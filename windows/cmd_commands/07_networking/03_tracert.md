
---
Displays the path packets take toward a destination.

### Syntax

```
tracert [-d] [-h maximum_hops] [-w timeout] [-4] [-6] target
```

### Basic

```
tracert google.com
```

Example:

```
1    1 ms    1 ms    1 ms  192.168.1.1
2   10 ms    8 ms    9 ms  ...
3   ...
```

Each numbered line represents a hop.

---

## `-d`

Don't resolve IP addresses to hostnames.

```
tracert -d google.com
```

This can make traceroute faster.

---

## `-h`

Maximum number of hops.

```
tracert -h 20 google.com
```

---

## `-w`

Timeout per reply:

```
tracert -w 1000 google.com
```

---

## `-4` / `-6`

```
tracert -4 google.com
```

```
tracert -6 google.com
```