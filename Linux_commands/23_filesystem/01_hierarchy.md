
---
Linux presents filesystems through a single directory tree:

```
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

The important concept is:

```
                    /
                    │
        ┌───────────┼───────────┐
        │           │           │
       /etc       /home       /var
        │           │           │
    configuration users       logs/data
```

Different physical filesystems can be mounted at different directories.