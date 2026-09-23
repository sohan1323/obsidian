
---
Python package manager.

It installs Python packages from package indexes such as PyPI.

### Check version

```
pip --version
```

or:

```
python3 -m pip --version
```

### Install package

```
python3 -m pip install requests
```

### Install specific version

```
python3 -m pip install requests==2.32.0
```

### Upgrade

```
python3 -m pip install --upgrade requests
```

### Uninstall

```
python3 -m pip uninstall requests
```

### List packages

```
python3 -m pip list
```

### Show package information

```
python3 -m pip show requests
```

### Important

For project work, prefer a virtual environment:

```
python3 -m venv .venv
source .venv/bin/activate
python -m pip install requests
```