
---
**Purpose:** Update the database used by `locate`.

### Syntax

```
updatedb [OPTIONS]
```

Usually:

```
sudo updatedb
```

Then:

```
locate filename
```

### Example

```
sudo updatedb
locate myfile.txt
```

### Important

If a file was recently created and:

```
locate myfile.txt
```

doesn't find it, the locate database may simply not have been updated.