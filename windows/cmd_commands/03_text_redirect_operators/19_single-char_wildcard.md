
---
`?` matches one character.

Example:

```
dir file?.txt
```

Could match:

```
file1.txt
file2.txt
fileA.txt
```

but not necessarily:

```
file10.txt
```

depending on matching behavior and filename format.

Another:

```
dir ?.txt
```

matches filenames with a single-character name before `.txt`.

---

