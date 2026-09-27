
---
Controls APT package selection states such as **manual** and **automatically installed**.

### Show automatically installed packages

```
apt-mark showauto
```

### Show manually installed packages

```
apt-mark showmanual
```

### Mark package as manually installed

```
sudo apt-mark manual nginx
```

This prevents APT from treating it as an automatically removable dependency.

### Mark as automatically installed

```
sudo apt-mark auto nginx
```

### Hold package

```
sudo apt-mark hold nginx
```

Prevent it from being upgraded.

### Unhold

```
sudo apt-mark unhold nginx
```