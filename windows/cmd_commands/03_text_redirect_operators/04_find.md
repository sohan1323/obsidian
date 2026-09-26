
---
Searches for a text string in files or command output.

### Syntax

```
find [/v] [/c] [/n] [/i] "string" [[drive:][path]filename]
```

### Important arguments

|Argument|Meaning|
|---|---|
|`/V`|Display lines that DON'T contain the string|
|`/C`|Count matching lines|
|`/N`|Display line numbers|
|`/I`|Case-insensitive search|
|`"string"`|Text to search for|

---

## Basic search

Create:

```
echo Hello World > test.txt
echo Windows CLI >> test.txt
echo PowerShell >> test.txt
```

Search:

```
find "Windows" test.txt
```

---

## `/I` — case insensitive

```
find /i "windows" test.txt
```

This matches:

```
Windows
WINDOWS
windows
```

---

## `/N` — line numbers

```
find /n "Windows" test.txt
```

Example:

```
---------- TEST.TXT
[2]Windows CLI
```

---

## `/C` — count matches

```
find /c "Windows" test.txt
```

---

## `/V` — lines NOT containing text

```
find /v "Windows" test.txt
```

This returns lines that don't contain `Windows`.