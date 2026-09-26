
---
Creates a Windows service.

### Syntax

```
sc create ServiceName [binPath= ...] [start= ...] [DisplayName= ...]
```

Example in a controlled lab:

```
sc create TestService binPath= "C:\Lab\TestService.exe"
```

With a display name:

```
sc create TestService binPath= "C:\Lab\TestService.exe" DisplayName= "Lab Test Service"
```

Automatic startup:

```
sc create TestService binPath= "C:\Lab\TestService.exe" start= auto
```

Manual startup:

```
sc create TestService binPath= "C:\Lab\TestService.exe" start= demand
```

Check it:

```
sc qc TestService
```