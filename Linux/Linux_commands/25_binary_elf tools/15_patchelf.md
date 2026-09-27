
---
`patchelf` modifies ELF binaries.

It may not be installed by default.

Check:

```
which patchelf
```

Display interpreter:

```
patchelf --print-interpreter ./program
```

Display RPATH:

```
patchelf --print-rpath ./program
```

Display needed libraries:

```
patchelf --print-needed ./program
```

Change interpreter:

```
patchelf --set-interpreter /path/to/loader ./program
```

Change RPATH:

```
patchelf --set-rpath /custom/lib ./program
```

Add dependency:

```
patchelf --add-needed libexample.so ./program
```

### Security/reversing use

Useful for analyzing:

```
ELF loaders
RPATH/RUNPATH
shared libraries
binary modification
```