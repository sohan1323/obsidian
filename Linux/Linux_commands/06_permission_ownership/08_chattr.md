
---
**Purpose:** Change filesystem attributes.

### Syntax

```
chattr [OPTIONS] MODE FILE
```

This generally requires root privileges for important attributes.

---

## Immutable attribute

Set immutable:

```
sudo chattr +i file.txt
```

Check:

```
lsattr file.txt
```

You may see:

```
----i----------------- file.txt
```

An immutable file cannot normally be modified, deleted, renamed, or linked to until the attribute is removed.

Remove immutable:

```
sudo chattr -i file.txt
```

Then normal modifications work again.

---

## Append-only

Set:

```
sudo chattr +a logfile
```

Remove:

```
sudo chattr -a logfile
```

An append-only file is designed so data can be appended but existing content cannot normally be modified through ordinary writes.