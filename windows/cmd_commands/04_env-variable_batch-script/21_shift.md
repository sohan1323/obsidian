
---
Moves batch arguments.

Suppose:

```
script.bat one two three four
```

Initially:

```
%1 = one
%2 = two
%3 = three
%4 = four
```

After:

```
shift
```

they become:

```
%1 = two
%2 = three
%3 = four
```

This is useful when processing an arbitrary number of arguments.