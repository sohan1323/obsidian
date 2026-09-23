
---
Tells systemd to reload unit-file configuration after changes.

```
sudo systemctl daemon-reload
```

Important:

> `daemon-reload` does not restart services.

You may then need:

```
sudo systemctl restart nginx
```