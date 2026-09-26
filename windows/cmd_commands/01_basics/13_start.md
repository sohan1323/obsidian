
---
Starts a program, command, document, directory, or another CMD window.

### Syntax

```
start ["title"] [/D path] [options] command
```

`start` has many options; the important ones are:

|Argument|Meaning|
|---|---|
|`"title"`|Window title|
|`/D path`|Starting directory|
|`/MIN`|Start minimized|
|`/MAX`|Start maximized|
|`/WAIT`|Wait for program to finish|
|`/B`|Start without creating a new window|
|`/LOW`|Start with low priority|
|`/NORMAL`|Normal priority|
|`/HIGH`|High priority|
|`/ABOVENORMAL`|Above normal priority|
|`/BELOWNORMAL`|Below normal priority|
|`/REALTIME`|Realtime priority|

### Open another CMD

```
start cmd
```

### Open Notepad

```
start notepad
```

### Open a directory

```
start C:\Users
```

### Open a website

```
start https://example.com
```

### Start minimized

```
start /min notepad
```

### Wait for program completion

```
start /wait notepad
```

CMD waits until Notepad exits.

### Important syntax trap

When the first argument is quoted, `start` treats it as the **window title**.

Therefore:

```
start "C:\Program Files\SomeApp\app.exe"
```

may not execute the program as you expect.

Use:

```
start "" "C:\Program Files\SomeApp\app.exe"
```

The empty `""` supplies the title.