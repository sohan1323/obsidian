
---


A filesystem can run out of:

```
disk blocks
```

or:

```
inodes
```

Check blocks:

```
df -h
```

Check inodes:

```
df -i
```

You can have free disk space but still be unable to create files if all inodes are exhausted.