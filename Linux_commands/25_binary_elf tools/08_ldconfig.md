
---
Manages the system's dynamic linker cache.

### Display cache

```
ldconfig -p
```

Search for a library:

```
ldconfig -p | grep libc
```

Example:

```
ldconfig -p | grep ssl
```

Configuration locations commonly include:

```
/etc/ld.so.conf
/etc/ld.so.conf.d/
```

Update cache:

```
sudo ldconfig
```

### Security relevance

Useful when investigating:

```
shared-library loading
library paths
dynamic linker configuration
```