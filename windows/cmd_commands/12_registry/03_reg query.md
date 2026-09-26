
---
`reg query` reads registry keys and values.

### Syntax

```
reg query KeyName
```

Example:

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion
```

---

## Query a specific value

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v ProgramFilesDir
```

`/v` specifies the value name.

---

## Query all values

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion
```