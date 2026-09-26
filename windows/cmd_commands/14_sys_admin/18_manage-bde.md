
---
`manage-bde` manages BitLocker from the command line.

### Show BitLocker status

```
manage-bde -status
```

Specific drive:

```
manage-bde -status C:
```

---

## Show BitLocker information

```
manage-bde -protectors -get C:
```

This displays configured BitLocker protectors.

---

## Suspend protection

```
manage-bde -protectors -disable C:
```

Resume:

```
manage-bde -protectors -enable C:
```

These operations should be performed only when required for legitimate administration because they affect disk protection.

# `manage-bde -on`

Enables BitLocker.

```
manage-bde -on D:
```

BitLocker configuration depends on the Windows edition, TPM configuration, recovery-key requirements, and organizational policy.

# `manage-bde -off`

Decrypts a BitLocker volume.

```
manage-bde -off D:
```

This can take substantial time.


# `manage-bde -unlock`

Unlocks an encrypted volume using an appropriate recovery/password mechanism.

Example with recovery password:

```
manage-bde -unlock D: -RecoveryPassword
```

Windows will prompt for the recovery password.

Avoid putting recovery secrets directly into command history.


# `manage-bde -protectors`

### List protectors

```
manage-bde -protectors -get C:
```

### Add a protector

The exact protector type determines the syntax, for example a recovery-password protector.

Because BitLocker configuration can affect system recoverability, test this on a VM or lab volume before automating it.

# `sc` vs `net`

We covered services previously.

Remember:

```
sc query
```

provides detailed service control functionality.

Whereas:

```
net start
```

provides a simpler service-management interface.