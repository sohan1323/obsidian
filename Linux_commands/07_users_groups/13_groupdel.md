
---
**Purpose:** Delete a group.

### Syntax

```
groupdel GROUP
```

Example:

```
sudo groupdel developers
```

### Important

You generally cannot delete a group that is currently the primary group of an existing user without first changing that user's primary group.