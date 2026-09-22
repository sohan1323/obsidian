
---
**Purpose:** Create a new group.

### Syntax

```
groupadd [OPTIONS] GROUP
```

### Example

```
sudo groupadd developers
```

Specify GID:

```
sudo groupadd -g 1500 developers
```

### Important options

| Option   | Meaning                                   |
| -------- | ----------------------------------------- |
| `-g GID` | Specify group ID                          |
| `-r`     | Create system group                       |
| `-f`     | Exit successfully if group already exists |