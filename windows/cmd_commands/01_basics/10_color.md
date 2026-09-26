
---
Changes CMD console foreground/background colors.

### Syntax

```
color [attr]
```

`attr` is a hexadecimal value:

```
Background + Foreground
```

### Color codes

|Code|Color|
|---|---|
|`0`|Black|
|`1`|Blue|
|`2`|Green|
|`3`|Aqua|
|`4`|Red|
|`5`|Purple|
|`6`|Yellow|
|`7`|White|
|`8`|Gray|
|`9`|Light Blue|
|`A`|Light Green|
|`B`|Light Aqua|
|`C`|Light Red|
|`D`|Light Purple|
|`E`|Light Yellow|
|`F`|Bright White|

### Examples

Green text:

```
color 0A
```

Black background + light green text.

Red text:

```
color 0C
```

White text:

```
color 07
```

### Important

The first digit is the background.

The second digit is the foreground.

For example:

```
color 1E
```

means:

```
1 = blue background
E = light yellow text
```