
---
Always quote paths that might contain spaces.

Bad:

```
cd C:\Program Files
```

Good:

```
cd /d "C:\Program Files"
```

Good:

```
copy "C:\My Files\test.txt" "C:\Backup\"
```

For variables:

```
set "FILE=C:\My Files\test.txt"

type "%FILE%"
```