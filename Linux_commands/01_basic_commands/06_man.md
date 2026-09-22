
---
**Purpose:** Opens the manual page for a command.

`man` is one of the most important commands to learn because you don't need to memorize every option.

### Syntax

```
man [SECTION] COMMAND
```

### Examples

```
man ls
```

Manual for `ls`.

```
man grep
```

Manual for `grep`.

Search for a keyword:

```
man -k network
```

This searches manual-page descriptions related to `network`.

Equivalent:

```
apropos network
```

### Useful options

|Option|Meaning|
|---|---|
|`-k keyword`|Search manual descriptions|
|`-f command`|Short description|
|`-a command`|Show all matching manual pages|

### Example

```
man -k password
```

### Inside `man`

|Key|Action|
|---|---|
|`Space`|Next page|
|`b`|Previous page|
|`/word`|Search|
|`n`|Next search result|
|`q`|Quit|

Example:

```
/recursive
```

Searches for `recursive`.