
---
Creates an override configuration for a systemd service.

```
sudo systemctl edit nginx
```

This creates an override rather than directly modifying the vendor unit file.

After modifying:

```
sudo systemctl daemon-reload
```

Then:

```
sudo systemctl restart nginx
```