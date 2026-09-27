
---
Resolves hostnames using the system's configured NSS mechanisms.

```
getent hosts example.com
```

Unlike `dig`, this tests the **system resolver path**.

### Compare

```
dig example.com
```

versus:

```
getent hosts example.com
```

This distinction can be useful when diagnosing local resolver configuration.