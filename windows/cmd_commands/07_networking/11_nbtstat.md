
---
Displays NetBIOS over TCP/IP information and statistics.

This is mostly relevant to legacy Windows networking and environments where NetBIOS remains enabled.

### Syntax

```
nbtstat [-a RemoteName] [-A IPAddress] [-c] [-n] [-r] [-R]
        [-s] [-S] [-RR] [-d] [-v]
```

---

## `-a`

Query a remote computer by name:

```
nbtstat -a COMPUTER01
```

---

## `-A`

Query by IP address:

```
nbtstat -A 192.168.1.20
```

---

## `-c`

Display NetBIOS name cache:

```
nbtstat -c
```

---

## `-n`

Display local NetBIOS names:

```
nbtstat -n
```

---

## `-r`

Display name-resolution statistics:

```
nbtstat -r
```

---

## `-S`

Display NetBIOS sessions using IP addresses.

```
nbtstat -S
```

---

## `-s`

Display sessions by remote computer name:

```
nbtstat -s
```
