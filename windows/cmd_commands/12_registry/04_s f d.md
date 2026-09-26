
---
Recursively query subkeys.

```
reg query HKLM\SOFTWARE\Microsoft /s
```

This can produce a very large amount of output.


# `/f`

Search for a string.

```
reg query HKLM\SOFTWARE\Microsoft /f "Windows"
```


# `/d`

Search the **data** of registry values.

```
reg query HKLM\SOFTWARE\Microsoft /f "C:\Windows" /d
```


# `/t`

Search only a specific registry value type.

Common types:

```
REG_SZ
REG_EXPAND_SZ
REG_MULTI_SZ
REG_DWORD
REG_QWORD
REG_BINARY
```

Example:

```
reg query HKLM\SOFTWARE\Microsoft /t REG_DWORD
```



# `/c`

Case-sensitive search.

```
reg query HKLM\SOFTWARE\Microsoft /f "Windows" /c
```

# `/e`

Exact-match search.

```
reg query HKLM\SOFTWARE\Microsoft /f "Windows" /e
```


# `/k`

Search key names.

```
reg query HKLM\SOFTWARE\Microsoft /f "Windows" /k
```