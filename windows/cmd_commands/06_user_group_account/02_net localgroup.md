
---
Displays and manages **local Windows groups**.

### Syntax

```
net localgroup
net localgroup groupname
net localgroup groupname username /add
net localgroup groupname username /delete
```

---

## List local groups

```
net localgroup
```

Common groups include:

```
Administrators
Users
Guests
Remote Desktop Users
Backup Operators
Remote Management Users
```

The exact groups vary by Windows edition/configuration.

---

## Display group members

```
net localgroup Administrators
```

Example:

```
Members

-------------------------------------------------------------------------------
Administrator
Sohan
```

This is an important command for understanding local privilege assignments.

---

## Add user to group

```
net localgroup Administrators TestUser /add
```

This gives `TestUser` membership in the local Administrators group.

**Be careful:** this grants substantial privileges.

---

## Remove user from group

```
net localgroup Administrators TestUser /delete
```

---

## Add user to another group

```
net localgroup "Remote Desktop Users" TestUser /add
```

Quotes are needed because the group name contains spaces.