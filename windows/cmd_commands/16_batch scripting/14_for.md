
---
`for` is one of the most important batch commands.

Basic syntax:

```
for %variable in (set) do command
```

Inside a `.bat` file:

```
for %%variable in (set) do command
```

Notice:

**Interactive CMD**

```
for %f in (*.txt) do echo %f
```

**Batch file**

```
for %%f in (*.txt) do echo %%f
```