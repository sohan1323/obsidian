
---
**Purpose:** Take input from standard input and use it as arguments to another command.

This is extremely useful when combining commands.

### Syntax

```
COMMAND1 | xargs COMMAND2
```

Example:

```
echo "file1 file2 file3" | xargs ls -l
```

Equivalent conceptually to:

```
ls -l file1 file2 file3
```

---

## Basic example

```
printf "one\ntwo\nthree\n" | xargs echo
```

Output:

```
one two three
```

---

## `find` + `xargs`

```
find . -type f -name "*.txt" -print0 | xargs -0 wc -l
```

### Why `-print0` and `-0`?

Normal whitespace separates arguments.

A filename can contain spaces:

```
my important file.txt
```

Using:

```
-print0
```

produces NUL-separated filenames.

Then:

```
xargs -0
```

correctly handles those filenames.

This is an important safe pattern.

---

## Important `xargs` options

|Option|Meaning|
|---|---|
|`-0`|Input items separated by NUL|
|`-n N`|Maximum N arguments per command|
|`-I {}`|Replace `{}` with input|
|`-P N`|Run N processes in parallel|
|`-r`|Don't run command if input is empty|

Example:

```
printf "a\nb\nc\n" | xargs -n 1 echo
```

Output:

```
a
b
c
```

Using replacement:

```
printf "a\nb\nc\n" | xargs -I {} echo "File: {}"
```

Output:

```
File: a
File: b
File: c
```

---

# `find -exec` vs `xargs`

Both can process files found by `find`.

### `-exec`

```
find . -type f -name "*.log" -exec grep "error" {} +
```

### `xargs`

```
find . -type f -name "*.log" -print0 | xargs -0 grep "error"
```

For complex commands, `find -exec` is often easier to reason about.

For bulk argument processing, `xargs` can be very useful.