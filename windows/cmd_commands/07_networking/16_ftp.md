
---
Interactive FTP client.

### Start

```
ftp
```

Connect:

```
ftp ftp.example.com
```

Common commands inside FTP:

```
open
user
ls
dir
cd
lcd
get
put
mget
mput
binary
ascii
delete
mkdir
rmdir
pwd
quit
```

Example:

```
ftp> open 192.168.1.10
ftp> user test
ftp> binary
ftp> get file.zip
ftp> quit
```

FTP transmits credentials/data without the protections provided by modern encrypted protocols, so use secure alternatives such as SFTP/HTTPS where appropriate.