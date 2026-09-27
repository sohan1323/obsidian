
---
**Purpose:** Display **Access Control Lists (ACLs)**.

ACLs allow more granular permissions than traditional owner/group/other permissions.

### Syntax

```
getfacl [OPTIONS] FILE
```

Example:

```
getfacl file.txt
```

Possible output:

```
# file: file.txt
# owner: alice
# group: developers
user::rw-
group::r--
other::---
```

---

## Why ACLs?

Traditional permissions allow:

```
owner
group
others
```

Suppose:

```
file.txt
```

belongs to:

```
alice:developers
```

but you also want `bob` to have read access without changing the primary group.

ACLs can do this.