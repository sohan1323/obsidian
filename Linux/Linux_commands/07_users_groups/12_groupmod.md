
---
**Purpose:** Modify an existing group.

### Syntax

```
groupmod [OPTIONS] GROUP
```

Rename:

```
sudo groupmod -n developers development
```

Change GID:

```
sudo groupmod -g 1600 developers
```

### Important options

| Option    | Meaning        |
| --------- | -------------- |
| `-n NAME` | New group name |
| `-g GID`  | New group ID   |