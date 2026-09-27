
---
Queries the local APT package database.

### Search

```
apt-cache search nginx
```

### Package information

```
apt-cache show nginx
```

### Package policy

```
apt-cache policy nginx
```

Example information:

```
Installed: 1.x
Candidate: 1.x
Version table:
```

### Dependencies

```
apt-cache depends nginx
```

Reverse dependencies:

```
apt-cache rdepends nginx
```

### Practical use

Determine which repository/version APT will install:

```
apt-cache policy nginx
```