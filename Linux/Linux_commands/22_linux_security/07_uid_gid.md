
---
Every process and user operates using numeric IDs.

Check:

```
id
```

Important IDs:

```
UID → User ID
GID → Group ID
```

Root normally has:

```
UID 0
```

Find UID 0 accounts:

```
awk -F: '$3 == 0 {print $1}' /etc/passwd
```