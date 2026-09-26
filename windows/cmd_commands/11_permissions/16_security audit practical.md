
---
For an authorized assessment, a useful workflow is:

### Current identity

```
whoami
```

### SID

```
whoami /user
```

### Groups

```
whoami /groups
```

### Privileges

```
whoami /priv
```

### Complete token information

```
whoami /all
```

### Inspect target ACL

```
icacls C:\Target
```

### Inspect recursively

```
icacls C:\Target /T
```

### Inspect owner

```
dir /q C:\Target
```

This helps answer:

```
Who am I?
     ↓
What groups do I have?
     ↓
What privileges do I have?
     ↓
Who owns the object?
     ↓
What ACL protects it?
     ↓
What access does my identity have?
```