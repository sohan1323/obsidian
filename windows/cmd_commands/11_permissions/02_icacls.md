
---
`icacls` is the primary modern CMD utility for viewing and modifying Windows file and directory ACLs.

---

## Basic usage

```
icacls C:\Lab
```

Example output:

```
C:\Lab BUILTIN\Administrators:(I)(F)
      NT AUTHORITY\SYSTEM:(I)(F)
      BUILTIN\Users:(I)(RX)
```

Common permission abbreviations:

|Permission|Meaning|
|---|---|
|`F`|Full control|
|`M`|Modify|
|`RX`|Read & execute|
|`R`|Read|
|`W`|Write|
|`D`|Delete|

Common inheritance flags:

| Flag | Meaning                      |
| ---- | ---------------------------- |
| `I`  | Inherited                    |
| `OI` | Object inherit               |
| `CI` | Container inherit            |
| `IO` | Inherit only                 |
| `NP` | Do not propagate inheritance |