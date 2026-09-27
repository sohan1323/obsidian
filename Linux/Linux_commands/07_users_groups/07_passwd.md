
---
**Purpose:** Change a user's password.

### Syntax

```
passwd [OPTIONS] [USER]
```

### Change your own password

```
passwd
```

You'll be prompted for:

```
Current password:
New password:
Retype new password:
```

### Change another user's password

Root/authorized administrator:

```
sudo passwd alice
```

### Lock an account

```
sudo passwd -l alice
```

### Unlock

```
sudo passwd -u alice
```

### Delete password

```
sudo passwd -d alice
```

⚠️ This can create an account with no password, depending on system authentication configuration. Don't use casually.

### Expire password

```
sudo passwd -e alice
```

This forces the user to change their password at next login.

### Important options

|Option|Meaning|
|---|---|
|`-l`|Lock account password|
|`-u`|Unlock|
|`-d`|Delete password|
|`-e`|Expire password|
|`-S`|Show password status|

Example:

```
sudo passwd -S alice
```