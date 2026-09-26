
---
Terminates running processes.

### Syntax

```
taskkill [/pid PID | /im ImageName] [/f] [/t]
```

### By PID

```
taskkill /pid 4820
```

### By process name

```
taskkill /im notepad.exe
```

### `/F`

Force termination:

```
taskkill /f /pid 4820
```

### `/T`

Terminates the specified process and its child processes.

```
taskkill /f /t /pid 4820
```

### Kill all instances of an executable

```
taskkill /f /im notepad.exe
```

### Combine

```
taskkill /f /t /im test.exe
```

Meaning:

```
/F → force
/T → include child processes
/IM → image name
```

### Important

Be careful with:

```
taskkill /f /im *.exe
```

or similarly broad patterns. Terminating critical Windows processes can destabilize the system.