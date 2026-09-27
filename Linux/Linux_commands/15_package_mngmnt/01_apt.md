
---
`apt` is the high-level package-management tool used on Debian-based systems such as:

- Debian
- Ubuntu
- Kali Linux

It handles:

- package installation
- package removal
- dependency resolution
- repository management
- package updates

### Syntax

```
sudo apt [COMMAND] [PACKAGE...]
```

---

## Update package lists

```
sudo apt update
```

This downloads the latest package metadata from configured repositories.

Important:

> `apt update` does **not** upgrade installed packages.

---

## Upgrade installed packages

```
sudo apt upgrade
```

Upgrades installed packages when possible without removing packages.

---

## Full upgrade

```
sudo apt full-upgrade
```

Allows more extensive dependency changes, including removing packages when required.

---

## Install package

```
sudo apt install nginx
```

Multiple packages:

```
sudo apt install curl wget git
```

---

## Remove package

```
sudo apt remove nginx
```

Removes the package but generally leaves configuration files.

---

## Purge package

```
sudo apt purge nginx
```

Removes the package and its system configuration files.

---

## Search packages

```
apt search nmap
```

Search package names/descriptions.

---

## Show package information

```
apt show nmap
```

Provides:

- version
- description
- dependencies
- package size
- repository
- installed status

---

## List installed packages

```
apt list --installed
```

Search installed packages:

```
apt list --installed | grep python
```

---

## List upgradeable packages

```
apt list --upgradable
```

---

## Remove unnecessary dependencies

```
sudo apt autoremove
```

Remove unused packages automatically installed as dependencies.

---

## Clean package cache

```
sudo apt clean
```

Removes downloaded package files from the local cache.

Less aggressive:

```
sudo apt autoclean
```