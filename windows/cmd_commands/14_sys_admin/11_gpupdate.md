
---
Refreshes Group Policy.

### Refresh policies

```
gpupdate
```

### Force refresh

```
gpupdate /force
```

### Computer policies

```
gpupdate /target:computer
```

### User policies

```
gpupdate /target:user
```

---

## Logoff after policy update

```
gpupdate /force /logoff
```

## Reboot after policy update

```
gpupdate /force /boot
```

Some policies require logoff or reboot before becoming effective.