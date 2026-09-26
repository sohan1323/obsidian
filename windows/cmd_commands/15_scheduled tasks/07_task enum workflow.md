
---
### Step 1 — List tasks

```
schtasks /query
```

### Step 2 — Get detailed information

```
schtasks /query /fo list /v
```

### Step 3 — Search output

```
schtasks /query /fo list /v | findstr /i "TaskName Task To Run Run As User"
```

### Step 4 — Inspect a specific task

```
schtasks /query /tn "\TaskName" /fo list /v
```

### Step 5 — Check referenced file

Suppose the task executes:

```
C:\Lab\backup.bat
```

Inspect it:

```
icacls C:\Lab\backup.bat
```

Check directory permissions:

```
icacls C:\Lab
```

