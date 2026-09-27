
---
A symbolic link stores a path to another file.

Create:

```
ln -s original.txt symlink.txt
```

Check:

```
ls -l symlink.txt
```

Example:

```
symlink.txt -> original.txt
```

Conceptually:

```
symlink
   │
   ▼
"path/to/file"
   │
   ▼
target
```




# Hard Link vs Symbolic Link

| Feature                       | Hard link | Symbolic link |
| ----------------------------- | --------- | ------------- |
| Same inode                    | Yes       | No            |
| Stores target path            | No        | Yes           |
| Can cross filesystems         | No        | Yes           |
| Can link directories normally | No        | Yes           |
| Broken if target name deleted | No        | Yes           |