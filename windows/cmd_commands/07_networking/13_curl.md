
---
Modern Windows includes `curl.exe`.

### Purpose

Makes HTTP/HTTPS and other network requests.

### Basic

```
curl https://example.com
```

### Save output

```
curl https://example.com -o page.html
```

### Follow redirects

```
curl -L https://example.com
```

### Display headers

```
curl -I https://example.com
```

### Verbose mode

```
curl -v https://example.com
```

### POST data

```
curl -X POST -d "name=test" https://example.com/api
```

Use POST examples only against systems where you have authorization to send requests.