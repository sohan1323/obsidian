
---
**Purpose:** Delete a user account.

### Syntax

```
userdel [OPTIONS] USERNAME
```

Basic:

```
sudo userdel alice
```

Remove user and home directory:

```
sudo userdel -r alice
```

### Important option

|Option|Meaning|
|---|---|
|`-r`|Remove home directory and mail spool|

### Important

Deleting an account does not necessarily remove every file owned by that UID elsewhere on the filesystem.

You can find such files with:

```
sudo find / -uid UID 2>/dev/null
```