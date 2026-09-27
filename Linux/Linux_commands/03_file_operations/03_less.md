
---
**Purpose:** View large files interactively without loading the entire file into your terminal at once.

### Syntax

```
less [OPTION] FILE
```

### Important options

|Option|Meaning|
|---|---|
|`-N`|Show line numbers|
|`-S`|Don't wrap long lines|
|`-i`|Ignore case during search|
|`-R`|Display raw terminal control characters|
|`-X`|Don't clear screen when exiting|

### Examples

```
less file.txt
```

With line numbers:

```
less -N file.txt
```

Don't wrap long lines:

```
less -S file.txt
```

### Important keys inside `less`

|Key|Action|
|---|---|
|`Space`|Next page|
|`b`|Previous page|
|`↑` / `↓`|Move line|
|`g`|Go to beginning|
|`G`|Go to end|
|`/text`|Search forward|
|`?text`|Search backward|
|`n`|Next match|
|`N`|Previous match|
|`q`|Quit|

### Example

```
less /var/log/auth.log
```

Then:

```
/failed
```

searches for `failed`.

### Practical cybersecurity use

Very commonly used for examining:

```
less /var/log/auth.log
```



