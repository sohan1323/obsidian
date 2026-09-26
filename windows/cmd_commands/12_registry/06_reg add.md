
---
Creates a registry key or adds/modifies a registry value.

### Syntax

```
reg add KeyName
```

Example:

```
reg add HKCU\Software\LabTest
```


# `/v`

Specifies the value name.

```
reg add HKCU\Software\LabTest /v TestValue
```


# `/t`

Specifies the value type.

Example:

```
reg add HKCU\Software\LabTest /v TestValue /t REG_SZ
```

Common types:

| Type            | Purpose           |
| --------------- | ----------------- |
| `REG_SZ`        | String            |
| `REG_EXPAND_SZ` | Expandable string |
| `REG_MULTI_SZ`  | Multiple strings  |
| `REG_DWORD`     | 32-bit integer    |
| `REG_QWORD`     | 64-bit integer    |
| `REG_BINARY`    | Binary data       |
# `/d`

Specifies the value's data.

Example:

```
reg add HKCU\Software\LabTest /v TestValue /t REG_SZ /d "Hello"
```

Now query:

```
reg query HKCU\Software\LabTest
```


# `/f`

Forces the operation without prompting.

```
reg add HKCU\Software\LabTest /v TestValue /t REG_SZ /d "Hello" /f
```

Use `/f` carefully when modifying existing configuration.


# Adding a `REG_DWORD`

```
reg add HKCU\Software\LabTest /v Enabled /t REG_DWORD /d 1
```

Query:

```
reg query HKCU\Software\LabTest /v Enabled
```

You might see:

```
Enabled    REG_DWORD    0x1
```


# Adding a `REG_QWORD`

```
reg add HKCU\Software\LabTest /v Number /t REG_QWORD /d 123456
```


# Adding a `REG_EXPAND_SZ`

```
reg add HKCU\Software\LabTest /v Path /t REG_EXPAND_SZ /d "%%PATH%%"
```

For environment-variable expansion, be aware that CMD batch files have their own `%` expansion rules.


# Adding a `REG_MULTI_SZ`

Multiple strings can be stored in a `REG_MULTI_SZ`.

```
reg add HKCU\Software\LabTest /v Servers /t REG_MULTI_SZ /d "Server1\0Server2\0Server3"
```

The exact encoding of multiple strings can be awkward from CMD; PowerShell is often easier for complex registry manipulation.