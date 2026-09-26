
---
Commands commonly return an exit code.

Conventionally:

```
0     → success
non-0 → failure/error
```

Example:

```
dir C:\Windows
echo %ERRORLEVEL%
```

If successful, you'll typically get:

```
0
```

Try:

```
dir C:\DoesNotExist
echo %ERRORLEVEL%
```

You should get a non-zero value.