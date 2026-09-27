
---
Creates and extracts archives in the **cpio** format.

### Create archive

```
find project/ -type f | cpio -ov > project.cpio
```

### Extract

```
cpio -idv < project.cpio
```

### List

```
cpio -itv < project.cpio
```

### Practical use

`cpio` is commonly encountered when working with:

- Linux initramfs
- system archives
- Unix/Linux backup formats