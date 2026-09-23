
---
Linux files can have extended attributes.

View them:

```
getfattr file.txt
```

Show all:

```
getfattr -d file.txt
```

Recursive:

```
getfattr -R -d directory/
```

Extended attributes can contain metadata used by applications and security mechanisms.