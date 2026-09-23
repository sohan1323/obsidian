
---
Lower-level command-line package-management interface.

`apt` is generally preferred for interactive use, while `apt-get` is commonly used in scripts and automation.

### Update

```
sudo apt-get update
```

### Upgrade

```
sudo apt-get upgrade
```

### Install

```
sudo apt-get install nginx
```

### Remove

```
sudo apt-get remove nginx
```

### Purge

```
sudo apt-get purge nginx
```

### Fix broken dependencies

```
sudo apt-get -f install
```

### Download package without installing

```
apt-get download nginx
```