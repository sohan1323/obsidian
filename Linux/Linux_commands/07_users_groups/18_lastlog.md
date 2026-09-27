
---
**Purpose:** Display the most recent login for each user.

### Syntax

```
lastlog [OPTIONS]
```

Example:

```
lastlog
```

Possible output:

```
Username    Port    From             Latest
root        **Never logged in**
alice       pts/0   192.168.1.20     Mon Sep 22
```

### Important options

|Option|Meaning|
|---|---|
|`-u USER`|Show specific user|
|`-t DAYS`|Show users who logged in within N days|

Example:

```
lastlog -u alice
```