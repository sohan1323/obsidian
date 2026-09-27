
---
`tar` creates and extracts **archives**.

Important distinction:

> `tar` primarily archives files. Compression is usually added with gzip, bzip2, or xz.

### Syntax

```
tar [OPTIONS] ARCHIVE FILES...
```

### Common options

|Option|Purpose|
|---|---|
|`-c`|Create archive|
|`-x`|Extract archive|
|`-t`|List contents|
|`-f`|Specify archive filename|
|`-v`|Verbose|
|`-z`|gzip compression|
|`-j`|bzip2 compression|
|`-J`|xz compression|
|`-C DIR`|Change directory before operation|
|`-p`|Preserve permissions|
|`--exclude`|Exclude files/directories|

---

### Create `.tar`

```
tar -cf backup.tar file1.txt file2.txt
```

Create archive from a directory:

```
tar -cf backup.tar project/
```

---

### List archive contents

```
tar -tf backup.tar
```

Verbose:

```
tar -tvf backup.tar
```

---

### Extract archive

```
tar -xf backup.tar
```

Extract into a specific directory:

```
tar -xf backup.tar -C /tmp
```

---

### Create gzip-compressed archive

```
tar -czf backup.tar.gz project/
```

Equivalent long extension commonly used:

```
.tar.gz
.tgz
```

Extract:

```
tar -xzf backup.tar.gz
```

List:

```
tar -tzf backup.tar.gz
```

---

### Create bzip2 archive

```
tar -cjf backup.tar.bz2 project/
```

Extract:

```
tar -xjf backup.tar.bz2
```

---

### Create xz archive

```
tar -cJf backup.tar.xz project/
```

Extract:

```
tar -xJf backup.tar.xz
```

---

### Exclude files

```
tar -czf backup.tar.gz project/ --exclude='*.log'
```

Exclude a directory:

```
tar -czf backup.tar.gz project/ --exclude='project/.git'
```

---

### Preserve permissions

```
sudo tar -cpzf backup.tar.gz /etc/
```

---

### Practical security use

Inspect an archive without extracting it:

```
tar -tzf backup.tar.gz
```

This is useful when examining a suspicious archive.