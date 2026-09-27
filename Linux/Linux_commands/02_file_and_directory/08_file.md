
---
**Purpose:** Determine the type of a file.

Linux does **not** rely solely on filename extensions to determine file types.

### Syntax

```
file [OPTION] FILE...
```

### Important options

|Option|Meaning|
|---|---|
|`-b`|Brief output|
|`-i`|Show MIME type|
|`-L`|Follow symbolic links|
|`-z`|Inspect compressed files|

### Examples

```
file document.pdf
```

Possible result:

```
document.pdf: PDF document
```

```
file image.jpg
```

```
image.jpg: JPEG image data
```

MIME type:

```
file -i document.pdf
```

### Security use

Very useful when investigating suspicious files:

```
file suspicious_file
```

A file named:

```
invoice.pdf
```

might actually be:

```
ELF 64-bit executable
```