
---
`sysctl` reads and modifies kernel parameters exposed through `/proc/sys`.

View all:

```
sysctl -a
```

Specific parameter:

```
sysctl net.ipv4.ip_forward
```

Example:

```
net.ipv4.ip_forward = 0
```

Temporarily change:

```
sudo sysctl -w net.ipv4.ip_forward=1
```

This changes the running kernel configuration.



# Important Security-Relevant `sysctl`

IPv4 forwarding:

```
sysctl net.ipv4.ip_forward
```

IPv6 forwarding:

```
sysctl net.ipv6.conf.all.forwarding
```

ASLR:

```
sysctl kernel.randomize_va_space
```

Check:

```
cat /proc/sys/kernel/randomize_va_space
```

Possible values commonly include:

```
0 → disabled
1 → partial randomization
2 → full randomization
```

These parameters are relevant when understanding Linux networking and exploit mitigations.



# Persistent `sysctl` Configuration

Runtime changes made with:

```
sudo sysctl -w ...
```

may not survive reboot.

Configuration can be stored under:

```
/etc/sysctl.conf
/etc/sysctl.d/
```

Inspect:

```
cat /etc/sysctl.conf
```

```
ls -la /etc/sysctl.d/
```

Apply configuration:

```
sudo sysctl -p
```