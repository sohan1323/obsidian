
---
**Purpose:** Search for files and directories based on conditions such as:

- Name
- Type
- Size
- Owner
- Group
- Permissions
- Modification time
- Access time
- Inode
- And more

### Syntax

```
find [PATH] [OPTIONS] [EXPRESSION]
```

Basic:

```
find /path -name "filename"
```

---

## Search by name

```
find /home -name "test.txt"
```

Search case-insensitively:

```
find /home -iname "test.txt"
```

Search using wildcards:

```
find /home -name "*.txt"
```

Find all `.conf` files:

```
find /etc -name "*.conf"
```

Find files beginning with `backup`:

```
find /home -name "backup*"
```

---

## Search directories

```
find /var -type d
```

`-type d` means directory.

Find regular files:

```
find /var -type f
```

Other useful types:

|Type|Meaning|
|---|---|
|`f`|Regular file|
|`d`|Directory|
|`l`|Symbolic link|
|`b`|Block device|
|`c`|Character device|
|`s`|Socket|
|`p`|Named pipe|

Example:

```
find /etc -type l
```

Find symbolic links under `/etc`.

---

## Search by size

Find files larger than 100 MB:

```
find / -type f -size +100M 2>/dev/null
```

Smaller than 10 MB:

```
find / -type f -size -10M 2>/dev/null
```

Exactly approximately 1 MB:

```
find . -type f -size 1M
```

### Size units

|Unit|Meaning|
|---|---|
|`c`|Bytes|
|`k`|KiB|
|`M`|MiB|
|`G`|GiB|

Example:

```
find /var/log -type f -size +500M
```

---

# Search by owner

Files owned by a particular user:

```
find /home -user alice
```

Files owned by `root`:

```
find / -user root 2>/dev/null
```

By group:

```
find /var -group adm
```

---

# Search by permissions

Find files with exactly `777` permissions:

```
find / -type f -perm 0777 2>/dev/null
```

Find files where **any execute bit** is set:

```
find . -type f -perm /111
```

Find files executable by the owner:

```
find . -type f -perm /100
```

Find SUID files:

```
find / -type f -perm -4000 2>/dev/null
```

Find SGID files:

```
find / -type f -perm -2000 2>/dev/null
```

These are particularly important during Linux privilege-escalation enumeration.

---

# Search by time

### `-mtime`

Modification time in **24-hour periods**.

Files modified within the last day:

```
find /var/log -type f -mtime -1
```

Files modified more than 7 days ago:

```
find /var/log -type f -mtime +7
```

Files modified exactly around 7 days ago:

```
find . -type f -mtime 7
```

### `-mmin`

Modification time in minutes.

Modified within the last 30 minutes:

```
find . -type f -mmin -30
```

Modified more than 60 minutes ago:

```
find . -type f -mmin +60
```

---

# `-atime` and `-amin`

Search based on **last access time**.

```
find . -type f -atime -1
```

Accessed within the last day.

```
find . -type f -amin -30
```

Accessed within the last 30 minutes.

---

# `-ctime` and `-cmin`

Search based on **inode/status change time**.

```
find . -type f -ctime -1
```

Changed within the last 24 hours.

Important: `ctime` is **not creation time** on normal Linux filesystems. It represents a change to filesystem metadata/status, such as permissions, ownership, or inode information.

---

# Combining conditions

AND:

```
find /var -type f -name "*.log" -size +100M
```

Find `.log` files larger than 100 MB.

Another:

```
find /home -type f -user alice -name "*.txt"
```

OR:

```
find . \( -name "*.jpg" -o -name "*.png" \)
```

Find `.jpg` **or** `.png`.

NOT:

```
find . -type f ! -name "*.txt"
```

Find files that aren't `.txt`.

---

# Search within a specific depth

Only current directory:

```
find . -maxdepth 1 -type f
```

Maximum two directory levels:

```
find . -maxdepth 2 -type f
```

Minimum depth:

```
find . -mindepth 2 -type f
```

Combined:

```
find . -mindepth 2 -maxdepth 3 -type f
```

---

# `find` with `-exec`

One of the most powerful features.

### Syntax

```
find PATH CONDITION -exec COMMAND {} \;
```

`{}` is replaced by the found filename.

`\;` terminates the `-exec` command.

Example:

```
find . -type f -name "*.txt" -exec cat {} \;
```

This runs:

```
cat file1.txt
cat file2.txt
cat file3.txt
```

for matching files.

---

## Run `ls`

```
find /var/log -type f -exec ls -lh {} \;
```

---

## Delete matching files

```
find . -type f -name "*.tmp" -delete
```

This is preferable to unnecessarily invoking `rm` through `-exec`.

Be careful:

```
find . -type f -name "*.tmp" -delete
```

actually deletes the matching files.

---

## Execute with multiple files at once

```
find . -type f -name "*.txt" -exec wc -l {} +
```

The `+` allows multiple files to be passed to one command invocation, which is generally more efficient than `\;`.

---

# `find` + `grep`

Search files containing a particular string:

```
find /etc -type f -name "*.conf" -exec grep -H "password" {} \; 2>/dev/null
```

This combines:

```
find → locate files
grep → search their contents
```

---

# Important cybersecurity `find` commands

Find SUID binaries:

```
find / -type f -perm -4000 2>/dev/null
```

Find SGID binaries:

```
find / -type f -perm -2000 2>/dev/null
```

Find world-writable files:

```
find / -type f -perm -002 2>/dev/null
```

Find world-writable directories:

```
find / -type d -perm -002 2>/dev/null
```

Find files writable by your user:

```
find / -type f -writable 2>/dev/null
```

Find files owned by your current user:

```
find / -type f -user "$(whoami)" 2>/dev/null
```

Find recently modified files:

```
find / -type f -mtime -1 2>/dev/null
```

Find SSH keys:

```
find /home -type f \( -name "id_rsa" -o -name "id_ed25519" \) 2>/dev/null
```

Find configuration files:

```
find /etc -type f -name "*.conf"
```