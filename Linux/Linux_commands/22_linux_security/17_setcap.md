
---
Assign a capability to a file.

Example:

```
sudo setcap cap_net_raw+ep ./program
```

Check:

```
getcap ./program
```

Remove:

```
sudo setcap -r ./program
```

Capabilities should be granted minimally because excessive capabilities can create security risks.