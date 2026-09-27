
---
Shows shared libraries required by a dynamically linked executable.

### Syntax

```
ldd FILE
```

Example:

```
ldd /bin/ls
```

Typical output:

```
libselinux.so.1
libc.so.6
libpcre2-8.so.0
/lib64/ld-linux-x86-64.so.2
```

Useful for determining:

```
Which libraries does this program depend on?
Which dynamic linker is being used?
```

---

## Check a program

```
ldd ./program
```

---

## Static binary

```
ldd ./static-program
```

May produce:

```
not a dynamic executable
```

---

## Security warning

Avoid using `ldd` on **untrusted executables**.

On some systems/conditions, mechanisms associated with dynamic loading can cause code execution when inspecting a malicious binary.

For safer inspection, use:

```
readelf -d ./program
```

or:

```
objdump -p ./program
```