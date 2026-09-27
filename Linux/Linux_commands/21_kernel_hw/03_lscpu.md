
---
Displays CPU architecture information.

```
lscpu
```

Important information:

```
Architecture
CPU(s)
Thread(s) per core
Core(s) per socket
Socket(s)
Model name
CPU MHz
Virtualization
```

Useful:

```
lscpu | grep -E "Architecture|CPU\(s\)|Model name|Virtualization"
```