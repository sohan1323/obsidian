
---
When Windows system files appear damaged:

### Step 1 — Check component store

```
DISM /Online /Cleanup-Image /CheckHealth
```

### Step 2 — Scan

```
DISM /Online /Cleanup-Image /ScanHealth
```

### Step 3 — Repair

```
DISM /Online /Cleanup-Image /RestoreHealth
```

### Step 4 — Verify protected files

```
sfc /scannow
```

### Step 5 — Check filesystem if necessary

```
chkdsk C: /scan
```

Conceptually:

```
DISM
 ↓
Windows component store
 ↓
SFC
 ↓
Protected system files
 ↓
CHKDSK
 ↓
Filesystem
```