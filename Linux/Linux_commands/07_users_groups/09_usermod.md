
---
**Purpose:** Modify an existing user account.

### Syntax

```
usermod [OPTIONS] USERNAME
```

---

## Change username

```
sudo usermod -l newname oldname
```

---

## Change home directory

```
sudo usermod -d /home/newhome alice
```

Move existing home contents too:

```
sudo usermod -d /home/newhome -m alice
```

---

## Change shell

```
sudo usermod -s /bin/zsh alice
```

---

## Add user to a supplementary group

```
sudo usermod -aG docker alice
```

### Very important

Use:

```
-aG
```

not just:

```
-G
```

because `-G` without `-a` replaces the user's supplementary group list.

---

## Remove user from a group

On many modern Linux systems:

```
sudo gpasswd -d alice docker
```

or use the appropriate distribution-specific group-management command.

---

## Lock account

```
sudo usermod -L alice
```

Unlock:

```
sudo usermod -U alice
```

### Important options

| Option | Meaning                  |
| ------ | ------------------------ |
| `-l`   | Change login name        |
| `-d`   | Change home directory    |
| `-m`   | Move home contents       |
| `-s`   | Change shell             |
| `-g`   | Change primary group     |
| `-G`   | Set supplementary groups |
| `-aG`  | Add supplementary groups |
| `-L`   | Lock                     |
| `-U`   | Unlock                   |
| `-u`   | Change UID               |