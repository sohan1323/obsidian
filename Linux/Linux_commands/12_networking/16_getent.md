
---
Queries system databases configured through **NSS (Name Service Switch)**.

It can query:

- hosts
- passwd
- group
- services
- networks

### Syntax

```
getent DATABASE [KEY]
```

### Examples

Resolve a hostname:

```
getent hosts example.com
```

Query local user database:

```
getent passwd
```

Specific user:

```
getent passwd root
```

Groups:

```
getent group
```

Services:

```
getent services ssh
```

### Practical security use

Enumerate users through the system's configured NSS sources:

```
getent passwd
```