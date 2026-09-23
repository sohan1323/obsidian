
---
Commands separated by `;` execute sequentially regardless of success.

```
command1; command2
```

Example:

```
pwd; ls; whoami
```

Even if `pwd` fails, Bash attempts `ls`.

Compare:

```
command1 && command2
```

which requires the first command to succeed.