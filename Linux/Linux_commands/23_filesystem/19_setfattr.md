
---
Set an extended attribute:

```
setfattr -n user.note -v "test" file.txt
```

Read:

```
getfattr -n user.note file.txt
```

Remove:

```
setfattr -x user.note file.txt
```