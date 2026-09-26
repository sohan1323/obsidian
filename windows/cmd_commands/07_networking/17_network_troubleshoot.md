
---
Suppose Windows cannot access a network resource.

Start with:

### Step 1 — Identify the machine

```
hostname
```

### Step 2 — Check adapter/IP configuration

```
ipconfig /all
```

### Step 3 — Check gateway

```
ipconfig
```

### Step 4 — Test local TCP/IP stack

```
ping 127.0.0.1
```

### Step 5 — Test local gateway

```
ping 192.168.1.1
```

Use your actual gateway address.

### Step 6 — Test external IP

```
ping 8.8.8.8
```

### Step 7 — Test DNS

```
nslookup example.com
```

### Step 8 — Test hostname connectivity

```
ping example.com
```

### Step 9 — Inspect route

```
route print
```

### Step 10 — Trace route

```
tracert example.com
```

### Step 11 — Inspect active connections

```
netstat -ano
```

### Step 12 — Identify the owning process

Suppose:

```
TCP 0.0.0.0:8080 ... LISTENING 4120
```

Then:

```
tasklist /fi "pid eq 4120"
```