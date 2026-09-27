
---
Provides an interactive file-transfer session over SSH.

### Syntax

```
sftp [OPTIONS] USER@HOST
```

Connect:

```
sftp user@192.168.1.10
```

### Common commands

|Command|Purpose|
|---|---|
|`ls`|Remote directory listing|
|`pwd`|Remote working directory|
|`cd`|Change remote directory|
|`lpwd`|Local working directory|
|`lcd`|Change local directory|
|`get`|Download|
|`put`|Upload|
|`mget`|Download multiple|
|`mput`|Upload multiple|
|`mkdir`|Create remote directory|
|`rm`|Delete remote file|
|`exit`|Exit|
|`help`|Help|

### Download

```
sftp> get file.txt
```

### Upload

```
sftp> put file.txt
```

### Download multiple files

```
sftp> mget *.log
```

### Practical use

SFTP is useful when you need interactive file transfer without giving shell access to a separate file-transfer service.