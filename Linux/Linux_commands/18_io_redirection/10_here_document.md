
---
Provides multiple lines of input to a command.

```
cat <<EOF
Hello
This is a
multi-line input
EOF
```

Output:

```
Hello
This is a
multi-line input
```

The delimiter can be any word:

```
cat <<END
Line 1
Line 2
END
```

---

# 16. Quoted Here Document

```
cat <<'EOF'
$USER
$(pwd)
EOF
```

Output literally contains:

```
$USER
$(pwd)
```

Quoting the delimiter prevents variable and command expansion.

Without quotes:

```
cat <<EOF
User: $USER
Directory: $(pwd)
EOF
```

Bash expands them.