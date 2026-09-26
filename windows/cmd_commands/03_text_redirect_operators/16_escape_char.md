
---
CMD uses `^` to escape special characters.

For example, these characters have special meanings:

```
&
|
>
<
^
```

If you want to print `>` literally:

```
echo ^>
```

Output:

```
>
```

Print `&`:

```
echo ^&
```

Print a pipe:

```
echo ^|
```

### Multiline commands

`^` can also continue a command onto the next line:

```
echo This is a very long ^
command
```

CMD treats it as one command.