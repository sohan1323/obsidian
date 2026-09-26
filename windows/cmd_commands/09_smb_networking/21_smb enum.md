
---
### Step 1 — Identify local computer

```
hostname
```

### Step 2 — View visible computers

```
net view
```

### Step 3 — Inspect a server

```
net view \\SERVER01
```

### Step 4 — Inspect available shares

```
net view \\SERVER01
```

### Step 5 — Access a share

```
dir \\SERVER01\Public
```

### Step 6 — Map it

```
net use Z: \\SERVER01\Public
```

### Step 7 — Verify

```
net use
```

### Step 8 — Disconnect

```
net use Z: /delete
```