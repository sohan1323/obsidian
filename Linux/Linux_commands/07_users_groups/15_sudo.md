
---
**Purpose:** Execute a command with elevated privileges or as another authorized user.

### Syntax

```
sudo [OPTIONS] COMMAND
```

Run command as root:

```
sudo systemctl restart ssh
```

Run as another user:

```
sudo -u alice whoami
```

Output:

```
alice
```

Open a root shell:

```
sudo -i
```

Run a root shell while retaining more of the current environment:

```
sudo -s
```

### Important options

|Option|Meaning|
|---|---|
|`-u USER`|Run as USER|
|`-i`|Login shell as target user|
|`-s`|Shell|
|`-l`|List allowed commands|
|`-k`|Invalidate cached credentials|
|`-v`|Update authentication timestamp|
|`-n`|Non-interactive|
|`-E`|Preserve environment where permitted|

### Check sudo permissions

```
sudo -l
```

This is particularly important during authorized Linux security assessments.

### `sudo` vs `su`

```
sudo command
```

Runs one command with elevated privileges.

```
su -
```

switches into another account's shell.