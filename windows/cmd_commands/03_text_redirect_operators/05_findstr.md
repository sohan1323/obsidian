
---
`findstr` is considerably more powerful than `find`.

It is one of the most useful CMD commands for **log analysis and security work**.

### Syntax

```
findstr [options] "search_string" [files]
```

---

## Basic search

```
findstr "error" application.log
```

---

## Case-insensitive

```
findstr /i "error" application.log
```

---

## Search multiple strings

```
findstr /i "error warning failed" application.log
```

This searches for lines matching the supplied search terms.

---

## `/S` — recursive search

```
findstr /s /i "password" *.txt
```

Searches `.txt` files in the current directory and subdirectories.

---

## `/N` — line numbers

```
findstr /n "error" application.log
```

Example:

```
42:Connection error
91:Database error
```

---

## `/V` — exclude matching lines

```
findstr /v /i "debug" application.log
```

Returns lines that don't match `debug`.

---

## `/M` — filenames only

```
findstr /m /i "password" *.txt
```

Instead of displaying matching lines, it displays filenames containing matches.

---

## `/C` — exact search string

```
findstr /c:"connection failed" application.log
```

Useful when searching for a phrase containing spaces.

---

## `/R` — regular expressions

`findstr` supports a limited regular-expression syntax.

Example:

```
findstr /r "[0-9][0-9][0-9]" file.txt
```

Searches for three consecutive digits.

---

## `/I /S /N`

You can combine options:

```
findstr /s /i /n "password" *.log
```

Meaning:

```
/S → recursive
/I → case-insensitive
/N → line numbers
```

---

## Search command output

This is where `findstr` becomes particularly useful.

```
ipconfig /all | findstr /i "IPv4"
```

Only lines containing `IPv4` are displayed.

Another example:

```
tasklist | findstr /i "chrome"
```

Find Chrome processes.

Another:

```
netstat -ano | findstr "LISTENING"
```

Find listening TCP connections.