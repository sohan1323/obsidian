
---
Identifies the type of a file.

### Syntax

```
file [OPTIONS] FILE
```

### Important options

|Option|Meaning|
|---|---|
|`-b`|Brief output|
|`-i`|MIME type|
|`-L`|Follow symbolic links|
|`-z`|Inspect compressed files|

### Examples

```
file /bin/bash
```

```
file ./program
```

```
file -b ./program
```

```
file -i ./program
```

### Security use

Quickly determine whether a downloaded file is:

```
ELF executable
Shell script
Python script
Shared library
Archive
Compressed file
```