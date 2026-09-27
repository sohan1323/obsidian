
---
**Purpose:** Display the groups a user belongs to.

### Syntax

```
groups [USER]
```

### Example

```
groups
```

Possible output:

```
sohan : sohan sudo docker
```

For another user:

```
groups alice
```

### Practical use

Check whether your user belongs to privileged groups:

```
groups
```

For example:

```
sohan : sohan sudo docker
```

Membership in groups such as `sudo` or, depending on system configuration, `docker` can have significant security implications.