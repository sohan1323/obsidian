
---
Manages volume mount points and volume GUID paths.

### List volumes

```
mountvol
```

You'll see entries similar to:

```
\\?\Volume{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}\
    C:\
```

### Remove a mount point

```
mountvol D: /D
```

### Create a mount point

```
mountvol D: \\?\Volume{GUID}\
```

Use caution when changing mount points because it can make volumes inaccessible through expected paths.