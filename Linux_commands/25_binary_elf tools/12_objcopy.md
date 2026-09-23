
---
Copies/converts object files and manipulates sections.

### Syntax

```
objcopy [OPTIONS] INPUT OUTPUT
```

Examples:

```
objcopy --only-section=.text program text.bin
```

Extract a section:

```
objcopy -O binary --only-section=.text program text.bin
```

Remove a section:

```
objcopy --remove-section=.comment program cleaned
```

### Common uses

```
extract sections
remove sections
convert formats
modify binary metadata
```