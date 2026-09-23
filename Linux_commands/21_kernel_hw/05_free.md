
---
Displays RAM and swap usage.

```
free
```

Human-readable:

```
free -h
```

Example:

```
               total   used   free
Mem:            15Gi    6Gi    4Gi
Swap:            2Gi    0Gi    2Gi
```

Options:

|Option|Purpose|
|---|---|
|`-h`|Human-readable|
|`-m`|MB|
|`-g`|GB|
|`-s N`|Repeat every N seconds|
|`-c N`|Repeat N times|
|`-t`|Include total|

Example:

```
free -h
```