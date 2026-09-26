
---
During authorized Windows assessment, storage information can reveal useful system context.

Examples:

### Identify mounted drives

```
fsutil fsinfo drives
```

### Identify volumes

```
mountvol
```

### Check filesystem

```
fsutil fsinfo volumeinfo C:
```

### Look for additional volumes

```
diskpart
```

then:

```
list disk
list volume
```

### Inspect filesystem change journal

```
fsutil usn queryjournal C:
```

This is particularly relevant to **Windows enumeration and forensic analysis**.