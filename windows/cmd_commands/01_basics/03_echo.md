
---
Displays text or controls command echoing.

### Syntax

```
echo [message]
```

or:

```
echo [on | off]
```

### Arguments

|Argument|Meaning|
|---|---|
|`message`|Text to display|
|`on`|Enable command echoing|
|`off`|Disable command echoing|

### Examples

```
echo Hello
```

Output:

```
Hello
```

Display an environment variable:

```
echo %USERNAME%
```

Example:

```
Sohan
```

Display current directory:

```
echo %CD%
```

Display PATH:

```
echo %PATH%
```

Check whether command echoing is enabled:

```
echo
```

Disable command echoing:

```
echo off
```

Enable it:

```
echo on
```

### Important in batch files

You'll frequently see:

```
@echo off
```

This prevents commands themselves from being displayed while the batch file runs.