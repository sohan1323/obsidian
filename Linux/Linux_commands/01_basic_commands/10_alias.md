
---
**Purpose:** Creates shortcuts for commands.

### Syntax

```
alias NAME='COMMAND'
```

### Examples

Create an alias:

```
alias ll='ls -lah'
```

Now:

```
ll
```

is equivalent to:

```
ls -lah
```

Another:

```
alias c='clear'
```

Now:

```
c
```

clears the terminal.

### Show aliases

```
alias
```

Show a specific alias:

```
alias ll
```

### Remove an alias

```
unalias ll
```

### Important

An alias created directly in the terminal normally lasts only for the current shell session.

To make it persistent, it is commonly placed in:

```
~/.bashrc
```

For example:

```
alias ll='ls -lah'
```

Then reload:

```
source ~/.bashrc
```