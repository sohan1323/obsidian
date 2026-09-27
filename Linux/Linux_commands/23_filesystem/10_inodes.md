
---
An **inode** stores filesystem metadata about a file.

It can contain information such as:

```
file type
permissions
owner
group
timestamps
file size
block references
```

The filename itself is associated with the inode through a directory entry.

Check inode:

```
ls -i file.txt
```

Example:

```
123456 file.txt
```

`123456` is the inode number.