
---
`DISM` = **Deployment Image Servicing and Management**.

It can inspect and repair the Windows component store.

### Check image health

```
DISM /Online /Cleanup-Image /CheckHealth
```

### Scan health

```
DISM /Online /Cleanup-Image /ScanHealth
```

### Repair health

```
DISM /Online /Cleanup-Image /RestoreHealth
```

The common repair sequence is:

```
DISM /Online /Cleanup-Image /RestoreHealth
sfc /scannow
```

# `/Online`

Specifies the currently running Windows installation.

```
DISM /Online /Cleanup-Image /CheckHealth
```

Instead of `/Online`, DISM can also work against offline Windows images.


# `/Image`

Specifies an offline Windows image.

Example:

```
DISM /Image:D:\ /Cleanup-Image /CheckHealth
```

This is primarily useful for recovery and Windows deployment work.


# `DISM /Get-CurrentEdition`

Shows the current Windows edition.

```
DISM /Online /Get-CurrentEdition
```

# `DISM /Get-TargetEditions`

Shows editions that the current installation can potentially be upgraded to:

```
DISM /Online /Get-TargetEditions
```


# `DISM /Get-Packages`

Lists installed Windows packages:

```
DISM /Online /Get-Packages
```

This can produce a large amount of output.


# `DISM /Get-Features`

Lists Windows optional features:

```
DISM /Online /Get-Features
```

Example filter:

```
DISM /Online /Get-Features | findstr /i "Hyper"
```


# `DISM /Enable-Feature`

Enables a Windows optional feature.

Example:

```
DISM /Online /Enable-Feature /FeatureName:TelnetClient
```

Restart if required:

```
DISM /Online /Enable-Feature /FeatureName:TelnetClient /All
```

Do not enable unnecessary Windows components on production systems.


# `DISM /Disable-Feature`

Disables an optional feature.

```
DISM /Online /Disable-Feature /FeatureName:TelnetClient
```