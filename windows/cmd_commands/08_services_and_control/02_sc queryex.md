
---
Provides extended service information.

### Syntax

```
sc queryex [ServiceName]
```

Example:

```
sc queryex Spooler
```

A useful field is:

```
PID : 1234
```

This lets you associate a service with its process.

Example:

```
sc queryex Spooler
```

Then:

```
tasklist /fi "PID eq 1234"
```