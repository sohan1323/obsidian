
---
Normally:

```
command1 | command2 | command3
```

The pipeline's exit status is usually the status of the **last command**.

Bash provides:

```
set -o pipefail
```

Now the pipeline fails if an earlier command fails.

Example:

```
set -o pipefail

cat missing.txt | grep hello
echo $?
```

The pipeline can now report failure instead of hiding the earlier error.