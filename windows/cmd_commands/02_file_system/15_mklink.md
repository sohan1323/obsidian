
---
Creates symbolic links and hard links.

This is an important Windows filesystem concept.

### Syntax

```
mklink [[/d] | [/h] | [/j]] Link Target
```

### Symbolic file link

```
mklink link.txt original.txt
```

Creates a symbolic link to a file.

### Directory symbolic link

```
mklink /d LinkFolder C:\RealFolder
```

### Hard link

```
mklink /h Link.txt Original.txt
```

A hard link references the same underlying file data.

### Junction

```
mklink /j LinkFolder C:\RealFolder
```

Creates a directory junction.

### Link types

|Command|Type|
|---|---|
|`mklink file target`|Symbolic file link|
|`mklink /d link target`|Directory symbolic link|
|`mklink /h link target`|Hard link|
|`mklink /j link target`|Junction|

### Practical example

```
mkdir C:\RealData
echo Hello > C:\RealData\test.txt
mklink /d C:\DataLink C:\RealData
```

Now:

```
dir C:\DataLink
```

shows the contents of:

```
C:\RealData
```