
---
If:

```
sudo apt install package
```

fails:

### Update repository metadata

```
sudo apt update
```

### Check package availability

```
apt-cache policy package
```

### Search

```
apt search package
```

### Check broken dependencies

```
sudo apt-get -f install
```

### Check package state

```
dpkg -l | grep package
```

### Check interrupted dpkg configuration

```
sudo dpkg --configure -a
```

Then:

```
sudo apt -f install
```