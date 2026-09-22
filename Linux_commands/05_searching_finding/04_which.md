
---
We already covered `which`, but it belongs here too because it's commonly used for finding executables.

### Syntax

```
which COMMAND
```

Example:

```
which python
```

Output might be:

```
/usr/bin/python
```

Multiple:

```
which python git nmap
```

### Limitation

`which` primarily answers:

> Which executable would be found through the current `PATH`?

It isn't a general filesystem search tool.

For example:

```
find / -name python 2>/dev/null
```

searches the filesystem instead.