
---
**Purpose:** Tells you **what kind of command** a command name represents.

### Syntax

```
type COMMAND
```

### Examples

```
type ls
```

Possible output:

```
ls is aliased to `ls --color=auto'
```

Another:

```
type cd
```

Output:

```
cd is a shell builtin
```

Another:

```
type python
```

Possible output:

```
python is /usr/bin/python
```

### Important options

```
type -a COMMAND
```

Show all locations/definitions.

Example:

```
type -a python
```

```
type -t COMMAND
```

Show only the command type.

Example:

```
type -t cd
```

Output:

```
builtin
```

### Common command types

A command can be:

```
alias
builtin
file
function
keyword
```