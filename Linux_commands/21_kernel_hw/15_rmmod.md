
---
Removes a loaded kernel module.

```
sudo rmmod module_name
```

If the module is being used, removal may fail.

Check:

```
lsmod | grep module_name
```


# Module Workflow

```
lsmod
   ↓
find module
   ↓
modinfo module
   ↓
check dependencies
   ↓
modprobe module
```

For example:

```
lsmod | grep e1000
```

```
modinfo e1000e
```