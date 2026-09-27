
---
Suppose port `8080` appears occupied.

First:

```
sudo ss -lntup | grep ':8080'
```

Then:

```
sudo lsof -i :8080
```

This identifies the process responsible.