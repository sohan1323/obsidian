
---
Loads or removes kernel modules while handling dependencies.

Load:

```
sudo modprobe module_name
```

Remove:

```
sudo modprobe -r module_name
```

Example:

```
sudo modprobe dummy
```

Then:

```
lsmod | grep dummy
```

`modprobe` is generally preferred over manually using `insmod` because it handles module dependencies.