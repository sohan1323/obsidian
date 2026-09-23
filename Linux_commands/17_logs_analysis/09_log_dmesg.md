
---
Some distributions maintain a saved copy of kernel messages here.

```
sudo less /var/log/dmesg
```

However, on modern systemd systems, `journalctl -k` is often the better source.