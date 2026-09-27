
---
Identifies processes using a file, directory, filesystem, or socket.

### Syntax

```
fuser [OPTION] [FILE]
```

### Examples

Find processes using `/mnt`:

```
sudo fuser -v /mnt
```

Find process using port 8080:

```
sudo fuser -v 8080/tcp
```

Kill processes using a mount:

```
sudo fuser -km /mnt
```

### Important options

|Option|Purpose|
|---|---|
|`-v`|Verbose|
|`-m`|Processes using filesystem|
|`-k`|Kill processes|
|`-n tcp`|TCP namespace|
|`-n udp`|UDP namespace|

Use `-k` carefully.