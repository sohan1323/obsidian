
---
`cacls` is an older ACL utility.

Example:

```
cacls C:\Lab
```

Grant read:

```
cacls C:\Lab /E /G Alice:R
```

Grant full control:

```
cacls C:\Lab /E /G Alice:F
```

Remove:

```
cacls C:\Lab /E /R Alice
```

### Important

`cacls` is **legacy**.

For modern Windows systems, prefer:

```
icacls
```