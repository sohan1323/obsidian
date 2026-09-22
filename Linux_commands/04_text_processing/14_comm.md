
---
**Purpose:** Compare two **sorted** files line by line.

### Syntax

```
comm [OPTIONS] FILE1 FILE2
```

Output has three columns:

```
Column 1 → only in FILE1
Column 2 → only in FILE2
Column 3 → in both
```

Example:

```
comm file1.txt file2.txt
```

### Important options

|Option|Meaning|
|---|---|
|`-1`|Hide column 1|
|`-2`|Hide column 2|
|`-3`|Hide column 3|

Show only lines common to both:

```
comm -12 file1.txt file2.txt
```

Show only lines unique to file 1:

```
comm -23 file1.txt file2.txt
```

### Important

Files should generally be sorted first:

```
sort file1.txt > sorted1.txt
sort file2.txt > sorted2.txt

comm sorted1.txt sorted2.txt
```