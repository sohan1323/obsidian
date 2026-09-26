
---
Displays and manages SMB shares on the local computer.

### List shares

```
net share
```

Example output might contain:

```
Share name   Resource
--------------------------------
ADMIN$       C:\Windows
C$           C:\
IPC$
Users        C:\Users
```

---

## Create a share

```
net share LabShare=C:\Lab
```

This shares:

```
C:\Lab
```

as:

```
\\COMPUTERNAME\LabShare
```

---

## Specify a comment

```
net share LabShare=C:\Lab /remark:"Laboratory Files"
```

---

## Remove a share

```
net share LabShare /delete
```

Important:

`net share ... /delete` removes the **share**, not necessarily the underlying directory.