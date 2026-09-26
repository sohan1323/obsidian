
---
Configures what happens when a service fails.

### Syntax

```
sc failure ServiceName [options]
```

Example:

```
sc failure MyService
```

Configure restart behavior:

```
sc failure MyService actions= restart/60000/restart/60000/""/60000
```

Here the actions specify what Windows should do after failures.

Common actions include:

```
restart
run
reboot
```