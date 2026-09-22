
---
### Headers

```
curl -I https://example.com
```

### Full request/response details

```
curl -v https://example.com
```

### Follow redirects

```
curl -IL https://example.com
```

### Test a specific HTTP method

```
curl -X OPTIONS https://example.com
```

### Send a custom Host header

```
curl -H "Host: example.com" http://192.168.1.10/
```

This is useful for testing virtual hosts on systems you are authorized to assess.

### Test HTTP response time

```
curl -o /dev/null -s -w '%{http_code} %{time_total}\n' https://example.com
```