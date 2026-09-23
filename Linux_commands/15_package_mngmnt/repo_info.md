
---
APT repositories are configured through files under:

```
/etc/apt/sources.list
/etc/apt/sources.list.d/
```

View the main configuration:

```
cat /etc/apt/sources.list
```

List additional repository files:

```
ls -la /etc/apt/sources.list.d/
```

Search repository configuration:

```
grep -R '^deb ' /etc/apt/sources.list /etc/apt/sources.list.d/ 2>/dev/null
```

Then update package metadata:

```
sudo apt update
```