
---
Displays or changes file attributes.

### Syntax

```
attrib [+attribute | -attribute] [drive:][path][filename] [/S] [/D] [/L]
```

### Attributes

|Attribute|Meaning|
|---|---|
|`R`|Read-only|
|`A`|Archive|
|`S`|System|
|`H`|Hidden|

### Display attributes

```
attrib
```

### Make file hidden

```
attrib +h secret.txt
```

### Remove hidden attribute

```
attrib -h secret.txt
```

### Make read-only

```
attrib +r important.txt
```

### Remove read-only

```
attrib -r important.txt
```

### Hidden + system

```
attrib +h +s file.txt
```

### Recursive

```
attrib +h /s *.txt
```

### Important security relevance

`attrib` only changes **attributes**.

It does **not** provide real access control.

For NTFS permissions, you'll later learn:

```
icacls
```