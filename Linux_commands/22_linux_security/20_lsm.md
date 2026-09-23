
---
Linux supports **Linux Security Modules (LSM)**.

Common implementations include:

```
AppArmor
SELinux
```

Check:

```
cat /sys/kernel/security/lsm
```

You may see something like:

```
capability,apparmor,...
```


# AppArmor

Check status:

```
sudo aa-status
```

List profiles:

```
sudo aa-status
```

AppArmor profiles are commonly stored under:

```
/etc/apparmor.d/
```

List:

```
ls -la /etc/apparmor.d/
```


On systems using SELinux:

```
getenforce
```

Possible output:

```
Enforcing
```

Other states:

```
Permissive
Disabled
```

Status:

```
sestatus
```

SELinux is common on distributions such as RHEL/Fedora, while Ubuntu commonly uses AppArmor.



# `aa-exec`

AppArmor can execute a program under a specified profile.

Example syntax:

```
sudo aa-exec -p profile-name -- command
```

This is primarily useful for administrators testing or applying AppArmor confinement.