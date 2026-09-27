APT stores downloaded package files under:

```
/var/cache/apt/archives/
```

Check size:

```
du -sh /var/cache/apt/archives/
```

Clean downloaded package files:

```
sudo apt clean
```

Check overall space:

```
df -h
```

This is particularly useful when an installation fails with:

```
No space left on device
```