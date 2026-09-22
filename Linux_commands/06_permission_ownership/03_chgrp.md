
---
**Purpose:** Change the group ownership of a file.

### Syntax

```
chgrp [OPTION] GROUP FILE...
```

Example:

```
sudo chgrp developers project.txt
```

Recursive:

```
sudo chgrp -R developers project/
```

### `chown` vs `chgrp`

```
chown alice file.txt
```

Changes owner.

```
chgrp developers file.txt
```

Changes group.

```
chown alice:developers file.txt
```

Changes both.