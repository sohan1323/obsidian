
---
```
set "name=Sohan"
echo %name%
```

CMD expands `%name%` before executing the command.

Example:

```
set "folder=C:\Lab"
mkdir "%folder%"
```

Quotes are important when paths contain spaces.