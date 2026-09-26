
---
Create:

```
hello.bat
```

Contents:

```
@echo off

echo Hello World
echo Current user: %USERNAME%
echo Computer: %COMPUTERNAME%

pause
```

Run:

```
hello.bat
```

### `@echo off`

```
@echo off
```

Stops CMD from displaying each command before executing it.

Without it:

```
C:\>echo Hello
Hello
```

With it:

```
Hello
```

### `@`

Suppresses display of that particular command.

```
@echo off
```

is effectively:

```
echo off
```

but the `echo off` command itself isn't displayed.