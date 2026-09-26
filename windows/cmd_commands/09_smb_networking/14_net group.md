
---
`net group` is primarily for **Active Directory domain groups**.

### List domain groups

```
net group /domain
```

### Inspect a domain group

```
net group "Domain Admins" /domain
```

### Add a domain user to a group

```
net group "Lab Group" alice /add /domain
```

### Remove

```
net group "Lab Group" alice /delete /domain
```

Administrative/domain permissions are required for modifications.