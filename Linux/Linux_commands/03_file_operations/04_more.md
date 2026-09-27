
---
**Purpose:** Display a file one screen at a time.

### Syntax

```
more [OPTION] FILE
```

### Examples

```
more file.txt
```

### Important options

|Option|Meaning|
|---|---|
|`-d`|Display helpful prompts|
|`-c`|Don't scroll; redraw screen|
|`-s`|Compress consecutive blank lines|
|`-n NUMBER`|Number of lines per screen|

Example:

```
more -n 20 file.txt
```

### `more` vs `less`

`more` is simpler.

`less` provides more navigation and searching capabilities.

For practical Linux work, **learn `less` more thoroughly**.