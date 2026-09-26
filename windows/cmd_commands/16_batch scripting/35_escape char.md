
---
CMD special characters include:

```
&
|
<
>
^
(
)
%
!
```

Escape many metacharacters with `^`.

Example:

```
echo Hello ^& World
```

Output:

```
Hello & World
```

Literal pipe:

```
echo A ^| B
```

Output:

```
A | B
```