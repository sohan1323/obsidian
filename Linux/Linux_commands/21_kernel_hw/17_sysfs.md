
---
`/sys` exposes kernel/device information through the **sysfs** filesystem.

```
ls /sys
```

Important areas:

```
/sys/class
/sys/devices
/sys/block
/sys/bus
/sys/module
```

Example:

```
ls /sys/class/net
```

Shows network interfaces.


# `/sys/class`

Provides device classes.

```
ls /sys/class
```

Examples:

```
/sys/class/net
/sys/class/block
/sys/class/tty
/sys/class/usb
```

Network interfaces:

```
ls /sys/class/net
```



# `/sys/class/net`

Inspect an interface:

```
ls /sys/class/net/eth0/
```

Interface state:

```
cat /sys/class/net/eth0/operstate
```

Possible output:

```
up
```

MAC address:

```
cat /sys/class/net/eth0/address
```


# `/sys/block`

Block devices:

```
ls /sys/block
```

You may see:

```
sda
nvme0n1
loop0
```

This is another way to inspect kernel device information.