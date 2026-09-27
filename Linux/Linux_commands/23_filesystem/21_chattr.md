
---
Change filesystem attributes.

Make a file immutable:

```
sudo chattr +i file.txt
```

Check:

```
lsattr file.txt
```

Remove:

```
sudo chattr -i file.txt
```

Append-only:

```
sudo chattr +a logfile
```

Remove:

```
sudo chattr -a logfile
```

`chattr` behavior depends on filesystem support.