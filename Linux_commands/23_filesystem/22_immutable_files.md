
---
An immutable file cannot normally be:

```
modified
deleted
renamed
```

while the immutable attribute is active.

Check:

```
lsattr important.txt
```

Example:

```
----i---------------- important.txt
```

Remove:

```
sudo chattr -i important.txt
```