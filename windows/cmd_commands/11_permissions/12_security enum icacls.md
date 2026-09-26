
---
Suppose you want to audit:

```
C:\Lab
```

Start with:

```
icacls C:\Lab
```

Then recursively:

```
icacls C:\Lab /T
```

Identify ownership:

```
dir /q C:\Lab
```

If ownership needs to be examined/managed:

```
takeown /f C:\Lab
```

Then inspect the ACL again:

```
icacls C:\Lab
```