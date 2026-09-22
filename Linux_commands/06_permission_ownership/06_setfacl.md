
---
**Purpose:** Add, modify, or remove ACL permissions.

### Syntax

```
setfacl [OPTIONS] ACL_SPEC FILE
```

Grant `bob` read permission:

```
setfacl -m u:bob:r file.txt
```

Check:

```
getfacl file.txt
```

Grant `bob` read/write:

```
setfacl -m u:bob:rw file.txt
```

Grant group permissions:

```
setfacl -m g:developers:rwx project/
```

---

## Remove an ACL

```
setfacl -x u:bob file.txt
```

Remove all extended ACLs:

```
setfacl -b file.txt
```

### Recursive ACL

```
setfacl -R -m u:bob:rX project/
```

`X` conditionally adds execute permission, typically when appropriate for directories or already-executable files.