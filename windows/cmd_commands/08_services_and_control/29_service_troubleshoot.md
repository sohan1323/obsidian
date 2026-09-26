
---
Suppose a service isn't working.

### Check state

```
sc query MyService
```

### Check configuration

```
sc qc MyService
```

### Check dependencies

```
sc enumdepend MyService
```

### Try starting it

```
sc start MyService
```

### Check again

```
sc query MyService
```

### Find the associated process

```
sc queryex MyService
```

Then:

```
tasklist /fi "PID eq 1234"
```