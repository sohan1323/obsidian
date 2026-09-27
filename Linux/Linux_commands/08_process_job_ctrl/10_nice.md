
---
**Purpose:** Start a process with a specified CPU scheduling priority.

Linux processes have a **niceness** value.

Typical range:

```
-20 → highest priority
  0 → default
+19 → lowest priority
```

### Syntax

```
nice [OPTION] [COMMAND]
```

Example:

```
nice -n 10 command
```

Start with niceness `10`.

```
nice -n 15 ./backup.sh
```

The backup process gets lower CPU scheduling priority relative to default-priority processes.

### Important option

| Option | Meaning                     |
| ------ | --------------------------- |
| `-n N` | Add/set niceness adjustment |