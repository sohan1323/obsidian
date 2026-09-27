
---
View currently mounted filesystems:

```
mount
```

More readable:

```
mount | column -t
```

Mount a filesystem:

```
sudo mount /dev/sdb1 /mnt
```

Specify filesystem type:

```
sudo mount -t ext4 /dev/sdb1 /mnt
```

# Mount Options

Mount options can modify filesystem behavior.

Example:

```
sudo mount -o ro /dev/sdb1 /mnt
```

`ro` means read-only.

Common options:

|Option|Meaning|
|---|---|
|`ro`|Read-only|
|`rw`|Read-write|
|`noexec`|Don't execute binaries|
|`nosuid`|Ignore SUID/SGID bits|
|`nodev`|Don't interpret device files|
|`noatime`|Don't update access times|

These options can be relevant to filesystem hardening.