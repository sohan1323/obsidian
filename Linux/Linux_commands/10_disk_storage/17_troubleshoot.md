
---
If a system says:

```
No space left on device
```

Use:

```
df -h
```

Then:

```
df -ih
```

Then identify large directories:

```
sudo du -xhd1 / | sort -h
```

Investigate likely locations:

```
sudo du -xhd1 /var | sort -h
```

Check large files:

```
sudo find /var -type f -size +500M -ls
```

If a filesystem is busy:

```
sudo lsof /mount/point
```

If using LVM:

```
sudo pvs
sudo vgs
sudo lvs
```