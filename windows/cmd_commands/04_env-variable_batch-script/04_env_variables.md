
---
Windows automatically provides many variables.

### `%USERNAME%`

```
echo %USERNAME%
```

Current username.

### `%USERPROFILE%`

```
echo %USERPROFILE%
```

Usually:

```
C:\Users\Sohan
```

### `%COMPUTERNAME%`

```
echo %COMPUTERNAME%
```

Computer hostname.

### `%SYSTEMROOT%`

```
echo %SYSTEMROOT%
```

Usually:

```
C:\Windows
```

### `%WINDIR%`

```
echo %WINDIR%
```

Windows directory.

### `%TEMP%`

```
echo %TEMP%
```

Current user's temporary directory.

### `%APPDATA%`

```
echo %APPDATA%
```

Roaming application data directory.

### `%LOCALAPPDATA%`

```
echo %LOCALAPPDATA%
```

Local application data.

### `%PROGRAMFILES%`

```
echo %PROGRAMFILES%
```

Typically:

```
C:\Program Files
```

### `%PROGRAMFILES(X86)%`

On 64-bit Windows:

```
echo %PROGRAMFILES(X86)%
```

Typically:

```
C:\Program Files (x86)
```

### `%CD%`

Current working directory.

```
echo %CD%
```

### `%DATE%`

```
echo %DATE%
```

### `%TIME%`

```
echo %TIME%
```

### `%ERRORLEVEL%`

Exit code from the previous command.

```
echo %ERRORLEVEL%
```