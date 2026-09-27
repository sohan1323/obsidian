
---
Generate a SHA-256 hash:

```
sha256sum file.txt
```

Verify against a checksum file:

```
sha256sum -c checksums.txt
```

Hashes are useful for verifying file integrity.

Other common commands:

```
md5sum file
sha1sum file
sha512sum file
```

For security-sensitive integrity verification, SHA-256 or stronger modern hashes are generally preferred over MD5/SHA-1.