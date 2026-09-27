
---
Directly inserts a kernel module.

```
sudo insmod module.ko
```

Unlike `modprobe`, it does not automatically resolve dependencies.

Because of this, `modprobe` is usually preferred.