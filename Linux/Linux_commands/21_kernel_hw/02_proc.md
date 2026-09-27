
---
`/proc` is a **virtual filesystem** provided by the kernel.

It exposes runtime information about:

```
processes
CPU
memory
kernel
devices
networking
system configuration
```

Check:

```
ls /proc
```

Important files:

```
/proc/cpuinfo
/proc/meminfo
/proc/version
/proc/uptime
/proc/loadavg
/proc/cmdline
```



# `/proc/cpuinfo`

Detailed CPU information:

```
cat /proc/cpuinfo
```

Useful:

```
grep "model name" /proc/cpuinfo
```

Count logical CPUs:

```
grep -c "^processor" /proc/cpuinfo
```


# `/proc/meminfo`

Memory information:

```
cat /proc/meminfo
```

Examples:

```
grep -E "MemTotal|MemFree|MemAvailable|SwapTotal|SwapFree" /proc/meminfo
```

This exposes kernel-level memory statistics.


# `/proc/version`

Kernel build information:

```
cat /proc/version
```

It can show:

```
kernel version
compiler
build information
```



# `/proc/uptime`

```
cat /proc/uptime
```

Example:

```
123456.78 987654.32
```

The first value represents system uptime in seconds.



# `/proc/loadavg`

```
cat /proc/loadavg
```

Example:

```
0.10 0.15 0.20 2/450 12345
```

The first three values represent load averages over:

```
1 minute
5 minutes
15 minutes
```



# `/proc/cmdline`

Shows kernel boot parameters:

```
cat /proc/cmdline
```

Example parameters can include:

```
root=
ro
quiet
splash
```

These are useful when investigating how the kernel was booted.