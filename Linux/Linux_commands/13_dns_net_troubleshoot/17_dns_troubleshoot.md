
---
Suppose:

```
ping example.com
```

fails.

### Step 1 — Test raw IP connectivity

```
ping -c 4 8.8.8.8
```

### Step 2 — Test DNS

```
dig example.com
```

### Step 3 — Check resolver configuration

```
resolvectl status
```

### Step 4 — Check `/etc/resolv.conf`

```
cat /etc/resolv.conf
```

### Step 5 — Query a known DNS server

```
dig @8.8.8.8 example.com
```

### Step 6 — Test system resolver

```
getent hosts example.com
```