
---
### Static linking

Libraries are included inside the executable.

```
program
 ├── code
 ├── libc code
 ├── other library code
 └── ...
```

Advantages:

```
fewer runtime dependencies
```

Disadvantages:

```
larger binary
```

---

### Dynamic linking

Libraries are loaded separately.

```
program
   ↓
dynamic linker
   ↓
libc.so
libm.so
libssl.so
...
```

Inspect dependencies:

```
ldd ./program
```

or:

```
readelf -d ./program
```