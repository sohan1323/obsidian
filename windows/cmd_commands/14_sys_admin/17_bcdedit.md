
---
`bcdedit` manages the Windows **Boot Configuration Data (BCD)** store.

### Display boot configuration

```
bcdedit
```

### Verbose listing

```
bcdedit /enum all
```

### Display boot manager

```
bcdedit /enum {bootmgr}
```

### Display current boot loader

```
bcdedit /enum {current}
```

BCD changes affect how Windows boots, so avoid experimenting on your primary installation.