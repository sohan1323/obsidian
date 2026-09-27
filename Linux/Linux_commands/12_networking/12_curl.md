
---
Transfers data using URLs.

It is extremely useful for **HTTP/HTTPS testing**.

### Syntax

```
curl [OPTIONS] URL
```

### Important options

|Option|Purpose|
|---|---|
|`-I`|Headers only|
|`-i`|Headers + body|
|`-v`|Verbose|
|`-s`|Silent|
|`-o FILE`|Save output|
|`-O`|Save using remote filename|
|`-L`|Follow redirects|
|`-X METHOD`|Specify HTTP method|
|`-H`|Add header|
|`-d`|Send request data|
|`-u`|HTTP authentication|
|`-k`|Ignore TLS certificate validation|

### Examples

GET request:

```
curl https://example.com
```

Headers only:

```
curl -I https://example.com
```

Verbose HTTP communication:

```
curl -v https://example.com
```

Follow redirects:

```
curl -L https://example.com
```

Save response:

```
curl -o response.html https://example.com
```

Specify header:

```
curl -H "User-Agent: test" https://example.com
```

POST data:

```
curl -X POST -d "username=test&password=test" https://example.com/login
```

JSON:

```
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"username":"test"}' \
  https://example.com/api
```

### Practical security use

Inspect HTTP response:

```
curl -i http://192.168.1.10
```

Inspect redirects:

```
curl -I -L http://example.com
```