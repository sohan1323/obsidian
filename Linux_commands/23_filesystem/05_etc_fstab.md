
---
Persistent filesystem mount configuration:

```
cat /etc/fstab
```

Typical format:

```
device  mountpoint  filesystem  options  dump  pass
```

Example:

```
UUID=xxxx  /data  ext4  defaults  0  2
```

The UUID can be obtained with:

```
blkid
```