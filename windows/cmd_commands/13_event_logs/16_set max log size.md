
---
Example:

```
wevtutil sl System /ms:104857600
```

`/ms` specifies maximum log size in bytes.

Here:

```
104857600 bytes ≈ 100 MB
```

Verify:

```
wevtutil gl System
```