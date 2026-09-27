
---
**Purpose:** Shows the executable that will be used when you run a command.

### Syntax

```
which COMMAND
```

### Examples

```
which python
```

Possible output:

```
/usr/bin/python
```

```
which bash
```

Output:

```
/usr/bin/bash
```

Multiple commands:

```
which python gcc git
```

### Important security relevance

`which` helps you understand **PATH resolution**.

For example:

```
which ls
```

tells you which `ls` executable your shell is likely to execute.