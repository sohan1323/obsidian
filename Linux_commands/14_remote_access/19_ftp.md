
---
Interactive client for the FTP protocol.

### Connect

```
ftp 192.168.1.10
```

Common commands:

|Command|Purpose|
|---|---|
|`ls`|List files|
|`cd`|Change remote directory|
|`pwd`|Show remote directory|
|`get`|Download|
|`put`|Upload|
|`mget`|Download multiple|
|`mput`|Upload multiple|
|`bye`|Exit|

### Important

FTP traditionally sends credentials and data without encryption.

For secure transfer, prefer:

```
SFTP
SCP
```