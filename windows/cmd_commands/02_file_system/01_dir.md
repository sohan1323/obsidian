
---
Lists files and directories.

### Syntax

```
dir [drive:][path][filename] [/a[[:]attributes]] [/b] [/c] [/d] [/l] [/n] [/o[[:]sortorder]] [/p] [/q] [/r] [/s] [/t[[:]timefield]] [/w] [/x] [/4]
```

### Basic usage

```
dir
```

Lists the current directory.

```
dir C:\Users
```

Lists `C:\Users`.

```
dir C:\Users\Sohan\Documents
```

Lists a specific directory.

---

## Important `dir` arguments

### `/A` — attributes

Controls which files are displayed.

```
dir /a
```

Shows all files, including hidden/system files.

You can specify attributes:

|Attribute|Meaning|
|---|---|
|`D`|Directories|
|`R`|Read-only|
|`H`|Hidden|
|`A`|Archive|
|`S`|System|
|`I`|Not content indexed|

Examples:

```
dir /a:d
```

Directories only.

```
dir /a:h
```

Hidden files.

```
dir /a:-h
```

Files that are **not** hidden.

```
dir /a:d /a:h
```

Hidden directories.

---

### `/B` — bare format

```
dir /b
```

Produces names without the normal metadata.

Example:

```
file1.txt
file2.txt
notes.txt
report.pdf
```

Very useful with scripts.

```
dir /b *.txt
```

Lists only `.txt` filenames.

---

### `/S` — recursive

```
dir /s
```

Searches the current directory and all subdirectories.

Example:

```
dir /s *.pdf
```

Finds PDFs recursively.

Very useful for locating files.

---

### `/P` — pagination

```
dir /p
```

Pauses when the screen is full.

Useful for large directories.

---

### `/W` — wide format

```
dir /w
```

Displays filenames in columns.

---

### `/O` — sorting

```
dir /o
```

Sorts output.

Common sorting options:

|Option|Sort by|
|---|---|
|`N`|Name|
|`E`|Extension|
|`S`|Size|
|`D`|Date/time|
|`G`|Directories first|
|`-`|Reverse order|

Examples:

```
dir /o:n
```

Sort by name.

```
dir /o:s
```

Sort by size.

```
dir /o:-s
```

Reverse size order.

```
dir /o:d
```

Sort by date.

```
dir /o:g
```

Directories first.

---

### `/T` — timestamp

Controls which timestamp is displayed.

```
dir /t:c
```

Creation time.

```
dir /t:a
```

Last access time.

```
dir /t:w
```

Last write time.

---

### `/Q` — owner

```
dir /q
```

Displays file ownership information.

Useful when investigating Windows permissions.

---

### `/R` — alternate data streams

```
dir /r
```

Displays alternate data streams associated with files.

This becomes relevant in Windows security investigations because NTFS supports **Alternate Data Streams (ADS)**.

---

### `/X` — short names

```
dir /x
```

Displays 8.3 short filenames where applicable.

---

### Combining switches

```
dir /a /s /b *.log
```

Meaning:

```
/a  → include all attributes
/s  → recursive
/b  → bare output
*.log → only LOG files
```

This is a very useful file-search pattern.