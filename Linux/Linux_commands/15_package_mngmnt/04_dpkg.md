
---
Low-level Debian package management.

Works directly with `.deb` packages.

### Syntax

```
dpkg [OPTIONS] ACTION
```

---

## List installed packages

```
dpkg -l
```

Search:

```
dpkg -l | grep nginx
```

---

## Show package information

```
dpkg -s nginx
```

---

## List files installed by a package

```
dpkg -L nginx
```

For example:

```
dpkg -L nginx | less
```

---

## Find which package owns a file

```
dpkg -S /usr/bin/curl
```

Example concept:

```
curl: /usr/bin/curl
```

This is extremely useful when you encounter an unfamiliar binary.

---

## Install `.deb`

```
sudo dpkg -i package.deb
```

If dependencies are missing:

```
sudo apt -f install
```

---

## Remove package

```
sudo dpkg -r package
```

---

## Purge package

```
sudo dpkg -P package
```