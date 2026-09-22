A general-purpose TCP/UDP networking utility.

It can:

- connect to ports
- listen on ports
- send data
- receive data
- test connectivity

### Syntax

```
nc [OPTIONS] HOST PORT
```

### Important options

|Option|Purpose|
|---|---|
|`-v`|Verbose|
|`-n`|Don't resolve DNS|
|`-z`|Scan without sending data|
|`-w N`|Timeout|
|`-l`|Listen|
|`-u`|UDP|
|`-p PORT`|Local port in implementations that support it|

### Test a TCP port

```
nc -vz 192.168.1.10 22
```

Test several ports:

```
nc -vz 192.168.1.10 20-25
```

Listen:

```
nc -lv 4444
```

Connect:

```
nc 192.168.1.10 4444
```

Then type text on either side.

### Practical security use

Basic service connectivity testing:

```
nc -vz 192.168.1.10 80
```