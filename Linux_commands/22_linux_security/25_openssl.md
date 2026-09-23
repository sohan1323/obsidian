
---
`openssl` is a general-purpose cryptographic/TLS command-line utility.

Check version:

```
openssl version
```

Inspect a TLS certificate:

```
openssl s_client -connect example.com:443
```

Extract certificate information:

```
openssl s_client -connect example.com:443 </dev/null 2>/dev/null \
    | openssl x509 -noout -subject -issuer -dates
```

This is useful for authorized TLS/security testing.