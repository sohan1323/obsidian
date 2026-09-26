
---
Changes the CMD command prompt.

Normally you'll see something like:

```
C:\Users\Sohan>
```

### Syntax

```
prompt [text]
```

CMD provides special prompt variables.

|Symbol|Meaning|
|---|---|
|`$P`|Current drive and path|
|`$G`|`>`|
|`$L`|`<`|
|`$B`|`|
|`$D`|Current date|
|`$T`|Current time|
|`$N`|Current drive|
|`$V`|Windows version|
|`$E`|Escape character|
|`$_`|Newline|

### Examples

Default-style prompt:

```
prompt $P$G
```

Result:

```
C:\Users\Sohan>
```

Show only the current directory:

```
prompt $P
```

Show date and time:

```
prompt $D $T$G
```

Example:

```
Thu 09/24/2026 10:45:32.12>
```

Reset to the normal prompt:

```
prompt $P$G
```

### Practical use

Useful when creating customized CMD environments or scripts.