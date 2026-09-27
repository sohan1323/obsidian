
---
**Purpose:** Create a new user account.

### Syntax

```
useradd [OPTIONS] USERNAME
```

### Basic example

```
sudo useradd alice
```

This creates the user account, but distribution-specific defaults determine exactly what gets created.

### Create home directory

```
sudo useradd -m alice
```

`-m` creates:

```
/home/alice
```

### Specify shell

```
sudo useradd -m -s /bin/bash alice
```

### Specify primary group

```
sudo useradd -m -g developers alice
```

### Add supplementary groups

```
sudo useradd -m -G sudo,docker alice
```

### Set UID

```
sudo useradd -u 1500 alice
```

### Important options

|Option|Meaning|
|---|---|
|`-m`|Create home directory|
|`-d DIR`|Specify home directory|
|`-s SHELL`|Specify login shell|
|`-g GROUP`|Primary group|
|`-G GROUPS`|Supplementary groups|
|`-u UID`|Specify UID|
|`-c COMMENT`|User description|
|`-e DATE`|Account expiration date|
|`-r`|Create system user|

### Typical command

```
sudo useradd -m -s /bin/bash alice
sudo passwd alice
```