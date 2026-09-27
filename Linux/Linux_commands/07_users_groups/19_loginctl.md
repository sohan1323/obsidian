
---
**Purpose:** Control and inspect systemd login sessions.

### Syntax

```
loginctl [COMMAND]
```

List sessions:

```
loginctl list-sessions
```

Show current session:

```
loginctl
```

Show user status:

```
loginctl user-status alice
```

Show session status:

```
loginctl session-status
```

List users:

```
loginctl list-users
```

Terminate a session:

```
sudo loginctl terminate-session SESSION_ID
```

### Practical use

Useful on systems using `systemd` for investigating:

- Login sessions
- User sessions
- Seats
- Session state

---

# Important Linux User Files

You should know these files because the commands above interact with them.

### `/etc/passwd`

Contains basic account information.

```
cat /etc/passwd
```

Typical entry:

```
alice:x:1001:1001:Alice:/home/alice:/bin/bash
```

Fields:

```
username
password placeholder
UID
GID
GECOS/comment
home directory
login shell
```

---

### `/etc/shadow`

Contains password-related authentication data and aging information.

```
sudo cat /etc/shadow
```

Access is normally restricted.

---

### `/etc/group`

Contains group information.

```
cat /etc/group
```

---

### `/etc/sudoers`

Controls sudo authorization.

```
sudo visudo
```

---

# Important UID Concepts

Common examples:

```
UID 0       → root
UID 1000+   → normal users on many distributions
```

Check:

```
id
```

Root:

```
id root
```

Output typically includes:

```
uid=0(root)
```

**Do not assume every Linux distribution uses exactly the same UID ranges for all account types.**

---

# Important Security Enumeration Commands

Current user:

```
whoami
```

Detailed identity:

```
id
```

Groups:

```
groups
```

Sudo privileges:

```
sudo -l
```

Current sessions:

```
w
```

Login history:

```
last
```

Last login per user:

```
lastlog
```

List local accounts:

```
cat /etc/passwd
```

Extract usernames:

```
cut -d ':' -f 1 /etc/passwd
```

Find users with interactive Bash shells:

```
grep '/bin/bash' /etc/passwd
```

Find files belonging to a UID:

```
find / -uid 1000 2>/dev/null
```