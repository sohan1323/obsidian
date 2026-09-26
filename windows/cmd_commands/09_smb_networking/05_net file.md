
---
Displays files opened through network shares.

### List open network files

```
net file
```

You may see:

```
ID     Path
-------------------------
12     C:\Shared\report.docx
```

---

## Close an open network file

```
net file 12 /close
```

This closes the network file associated with ID `12`.