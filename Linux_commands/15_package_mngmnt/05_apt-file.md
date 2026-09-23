
---
Searches package contents, including files from packages that are not currently installed.

It may need to be installed first:

```
sudo apt install apt-file
```

Update its database:

```
sudo apt-file update
```

Search for a file:

```
apt-file search bin/nmap
```

### Practical use

Suppose a program requires:

```
libexample.so
```

You can search which package provides it:

```
apt-file search libexample.so
```