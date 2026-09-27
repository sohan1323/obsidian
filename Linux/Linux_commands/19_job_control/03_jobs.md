
---
Displays jobs belonging to the current shell.

```
jobs
```

Example:

```
[1]+  Running    sleep 60 &
[2]-  Stopped    vim file.txt
```

### Options

|Option|Purpose|
|---|---|
|`-l`|Show PID|
|`-p`|Show process IDs|
|`-r`|Running jobs|
|`-s`|Stopped jobs|

Example:

```
jobs -l
```