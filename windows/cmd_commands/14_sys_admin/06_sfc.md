
---
`SFC` = **System File Checker**

Checks protected Windows system files.

### Scan

```
sfc /scannow
```

This is one of the most important Windows repair commands.


## Verify only

```
sfc /verifyonly
```

This checks integrity without attempting repairs.

---

## Scan a specific file

```
sfc /scanfile=C:\Windows\System32\example.dll
```

---

## Verify a specific file

```
sfc /verifyfile=C:\Windows\System32\example.dll
```