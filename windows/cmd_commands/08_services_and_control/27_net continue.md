
---
Resumes a paused service.

```
net continue MyService
```




# Service Name vs Display Name

This distinction is extremely important.

Example:

```
Service Name:  Spooler
Display Name:  Print Spooler
```

With `sc`:

```
sc query Spooler
```

With `net`:

```
net stop "Print Spooler"
```

You can discover the mapping with:

```
sc getdisplayname Spooler
```

and:

```
sc getkeyname "Print Spooler"
```