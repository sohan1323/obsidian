
---
A useful Windows administration sequence is:

### Identity

```
whoami /all
```

### Host

```
hostname
```

### OS

```
systeminfo
```

### Network

```
ipconfig /all
```

### Processes

```
tasklist /svc
```

### Services

```
sc query
```

### Storage

```
fsutil fsinfo drives
```

### Group Policy

```
gpresult /r
```

### Drivers

```
driverquery
```

### Event logs

```
wevtutil el
```

### Security auditing

```
auditpol /get /category:*
```