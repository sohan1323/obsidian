
---
**HTTP** stands for **Hypertext Transfer Protocol**. It’s the set of rules web browsers and servers use to communicate over the internet.

# HTTP Request

An **HTTP request** is a message sent by a **client** (usually your browser) to a **web server** asking it to perform some action or return some resource.

For example, when you open:

```
https://example.com/login
```

your browser sends an HTTP request to the server.

## Structure of an HTTP Request

An HTTP request generally contains:

```
Request Line
Headers
Blank Line
Body (optional)
```

Example:

```
POST /login HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Cookie: session=abc123

username=admin&password=test123
```

Let's break it down.

### 1. Request Line

```
POST /login HTTP/1.1
```

It contains three important parts:

```
POST      /login       HTTP/1.1
 │           │             │
Method      Path        HTTP version
```

**Method** tells the server what operation you want.

Common methods:

|Method|Purpose|
|---|---|
|GET|Retrieve data|
|POST|Send/create data|
|PUT|Replace/update data|
|PATCH|Partially update data|
|DELETE|Delete data|
|HEAD|Get headers without response body|
|OPTIONS|Ask what methods/options are supported|
|TRACE|Diagnostic request; often disabled|

For bug bounty, **GET, POST, PUT, PATCH and DELETE** are especially important.

---

## 2. Request Target / Path

Example:

```
GET /products/123 HTTP/1.1
```

Here:

```
/products/123
```

is the requested resource/path.

It can also contain query parameters:

```
GET /search?q=laptop&page=2 HTTP/1.1
```

Here:

```
q=laptop
page=2
```

are **query parameters**.

---

## 3. HTTP Headers

Headers provide additional information about the request.

Example:

```
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
Cookie: session=abc123
Content-Type: application/json
Authorization: Bearer eyJ...
```

Important headers to learn for web security:

- `Host`
- `User-Agent`
- `Accept`
- `Content-Type`
- `Content-Length`
- `Cookie`
- `Authorization`
- `Referer`
- `Origin`
- `Content-Encoding`
- `X-Forwarded-For`
- `X-Forwarded-Host`
- `X-Forwarded-Proto`

These become particularly important when learning **Burp Suite, authentication, sessions, CSRF, SSRF, CORS, host-header attacks, and request smuggling**.

---

## 4. Request Body

The body contains data sent to the server.

For example:

```
POST /login HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded

username=admin&password=test123
```

The body is:

```
username=admin&password=test123
```

A JSON API might instead send:

```
POST /api/login HTTP/1.1
Host: example.com
Content-Type: application/json

{
    "username": "admin",
    "password": "test123"
}
```

Not every request has a body.

For example, a typical `GET` request usually doesn't need one.

# HTTP Response

An **HTTP response** is the message that a **web server sends back to the client** after receiving and processing an HTTP request.

The basic communication is:

```
Client / Browser
      │
      │ HTTP Request
      ▼
   Web Server
      │
      │ HTTP Response
      ▼
Client / Browser
```

For example, you request:

```
GET /login HTTP/1.1
Host: example.com
```

The server might respond:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1250

<html>
    <body>
        <h1>Login</h1>
    </body>
</html>
```

---

# Structure of an HTTP Response

An HTTP response consists mainly of:

```
Status Line
Headers
Blank Line
Body
```

Example:

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 45
Set-Cookie: session=abc123

{
    "message": "Login successful"
}
```

Let's break it down.

---

## 1. Status Line

The first line is the **status line**:

```
HTTP/1.1 200 OK
```

It contains:

```
HTTP/1.1     200       OK
   │           │        │
Version    Status     Reason
           Code       Phrase
```

The **status code** tells the client what happened.

### Important status codes

|Code|Meaning|Example|
|---|---|---|
|**200**|OK / successful|Page loaded successfully|
|**201**|Created|New account/resource created|
|**204**|No Content|Request succeeded, nothing to return|
|**301**|Permanent Redirect|Resource moved permanently|
|**302**|Temporary Redirect|Redirect to another location|
|**304**|Not Modified|Browser can use cached version|
|**400**|Bad Request|Invalid request|
|**401**|Unauthorized|Authentication required/failed|
|**403**|Forbidden|Server refuses access|
|**404**|Not Found|Resource doesn't exist|
|**405**|Method Not Allowed|HTTP method isn't supported|
|**429**|Too Many Requests|Rate limit exceeded|
|**500**|Internal Server Error|Server-side error|
|**502**|Bad Gateway|Gateway/proxy received bad response|
|**503**|Service Unavailable|Server temporarily unavailable|

For bug bounty, **401, 403, 404, 405, 429 and 500** are particularly useful to understand because they can provide clues about application behavior.

---

# 2. Response Headers

Headers provide additional information about the response.

Example:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 5230
Server: nginx
Set-Cookie: session=abc123; Secure; HttpOnly
Cache-Control: no-cache
```

Important response headers include:

### `Content-Type`

Tells the browser what type of content is being returned.

```
Content-Type: text/html
```

Other examples:

```
Content-Type: application/json
Content-Type: text/css
Content-Type: image/png
```

---

### `Content-Length`

Specifies the size of the response body.

```
Content-Length: 5230
```

---

### `Set-Cookie`

Used by the server to create/update a cookie in the browser.

```
Set-Cookie: session=abc123; Secure; HttpOnly
```

This is extremely important when learning **session management and authentication security**.

---

### `Location`

Usually used with redirects.

```
HTTP/1.1 302 Found
Location: /dashboard
```

The browser will typically request:

```
/dashboard
```

---

### `Server`

May reveal information about the server software:

```
Server: nginx
```

or:

```
Server: Apache
```

This can sometimes provide useful information during reconnaissance, although modern applications may hide or modify it.

---

### Security Headers

You will frequently encounter:

```
Content-Security-Policy: ...
Strict-Transport-Security: ...
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: ...
Permissions-Policy: ...
```

These are important when studying **web security and defensive controls**.

---

# 3. Response Body

The body contains the actual data returned by the server.

For example, HTML:

```
HTTP/1.1 200 OK
Content-Type: text/html

<html>
    <h1>Welcome</h1>
</html>
```

JSON:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "id": 123,
    "username": "admin"
}
```

An image:

```
HTTP/1.1 200 OK
Content-Type: image/png

[binary image data]
```

The response body is therefore **not necessarily HTML**. It can be JSON, XML, JavaScript, an image, a PDF, binary data, etc.


# HTTP Request/Response Model

The **request/response model** is the fundamental communication model used by HTTP.

The basic idea is simple:

> **A client sends a request → a server processes it → the server sends a response back.**


---

## 1. Client

The **client** initiates communication.

Examples:

- Web browser
- Mobile application
- `curl`
- Postman
- Burp Suite
- Python program
- JavaScript application

For example, you enter:

```
https://example.com/products
```

Your browser becomes the HTTP client and sends a request.

---

## 2. HTTP Request

The client sends an HTTP request to the server.

Example:

```
GET /products HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

The request essentially says:

> "Server, I want the `/products` resource."

A request can contain:

```
Method
URL / Path
Headers
Query Parameters
Cookies
Request Body
```

---

## 3. Server

The **server** receives the request.

The server may perform several operations:

```
Receive request
      ↓
Parse request
      ↓
Authenticate user
      ↓
Check authorization
      ↓
Validate input
      ↓
Run application logic
      ↓
Query database
      ↓
Generate response
```

For example:

```
GET /products/123
        ↓
Application receives request
        ↓
Look for product ID 123
        ↓
Query database
        ↓
Product found
        ↓
Generate response
```

---

## 4. HTTP Response

The server sends an HTTP response back to the client.

Example:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "id": 123,
    "name": "Laptop",
    "price": 75000
}
```

The response contains:

```
Status Code
Headers
Response Body
```

The client then uses the response.

For a browser, it might render an HTML page.

For an API client, it might process JSON.

# HTTP Is Stateless

One important characteristic of HTTP is that it is generally **stateless**.

For example:

```
Request 1:
GET /login

Request 2:
POST /login

Request 3:
GET /profile
```

The server doesn't inherently have HTTP-level memory saying:

> "This is the same person who made Request 1."

Applications implement state using mechanisms such as:

- Cookies
- Session IDs
- Tokens
- JWTs
- Authentication headers

# HTTP Methods

**HTTP methods** tell the server **what operation the client wants to perform on a resource**.

## 1. GET

Used to **retrieve/read data**.

```
GET /users/123 HTTP/1.1
Host: example.com
```

Meaning:

> Give me user 123.

Typical uses:

```
GET /products
GET /products/123
GET /profile
GET /search?q=laptop
```

Usually, GET parameters are placed in the URL:

```
/search?q=laptop&page=2
```

### Important property

GET is intended to be **safe** and **idempotent**.

It should not normally modify server-side data.

---

# 2. POST

Used to **submit data** or request creation/action.

```
POST /users HTTP/1.1
Host: example.com
Content-Type: application/json

{
    "username": "john",
    "email": "john@example.com"
}
```

The server might create a new user.

Another example:

```
POST /login HTTP/1.1

username=john&password=secret
```

Common uses:

- Login
- Registration
- Form submission
- Creating resources
- File uploads
- Sending data to an API

Unlike GET, POST commonly carries data in the **request body**.

---

# 3. PUT

Used to **replace/update a resource**.

Example:

```
PUT /users/123 HTTP/1.1
Content-Type: application/json

{
    "username": "john",
    "email": "new@example.com",
    "role": "user"
}
```

Conceptually:

```
Existing resource
       ↓
    Replace
       ↓
Updated resource
```

PUT is generally **idempotent**.

If you send the same PUT request multiple times, the intended final state should be the same.

---

# 4. PATCH

Used to **partially modify a resource**.

Suppose the existing user is:

```
{
    "username": "john",
    "email": "john@example.com",
    "role": "user"
}
```

You only want to change the email:

```
PATCH /users/123 HTTP/1.1
Content-Type: application/json

{
    "email": "new@example.com"
}
```

Only the specified field is changed.

### PUT vs PATCH

```
PUT
Replace the resource
        ↓
[username, email, role] → [new username, new email, new role]

PATCH
Modify part of the resource
        ↓
[username, email, role]
        ↓
         email changed
```

---

# 5. DELETE

Used to **delete a resource**.

```
DELETE /users/123 HTTP/1.1
Host: example.com
```

Meaning:

> Delete user 123.

A successful response might be:

```
HTTP/1.1 204 No Content
```

---

# 6. HEAD

`HEAD` is similar to `GET`, but the server returns **headers without the response body**.

```
HEAD /index.html HTTP/1.1
Host: example.com
```

Possible response:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 5420
Last-Modified: ...
```

Useful for:

- Checking whether a resource exists
- Checking response headers
- Checking resource size
- Testing server behavior without downloading the body

---

# 7. OPTIONS

Used to ask the server what communication options/methods are available for a resource.

```
OPTIONS /api/users HTTP/1.1
Host: example.com
```

Possible response:

```
HTTP/1.1 204 No Content
Allow: GET, POST, PUT, PATCH, DELETE, OPTIONS
```

This tells you that those methods are allowed for that resource.

`OPTIONS` is also important when studying **CORS** and browser preflight requests.

---

# 8. TRACE

Used for diagnostic purposes. The server may return the received request.

```
TRACE / HTTP/1.1
Host: example.com
```

TRACE is commonly **disabled** on production servers because it can create security concerns, historically including issues related to Cross-Site Tracing (XST).

For bug bounty, you may encounter:

```
HTTP/1.1 405 Method Not Allowed
```

if it is disabled.

---

# 9. CONNECT

Used to establish a **tunnel** through an HTTP proxy, most commonly for HTTPS.

Example:

```
CONNECT example.com:443 HTTP/1.1
Host: example.com:443
```

The proxy establishes a TCP tunnel to the destination.

You generally won't use CONNECT directly during normal web application testing.


# HTTP Versions

**HTTP versions** are different generations of the HTTP protocol. Each version improved how clients and servers communicate, mainly in terms of **performance, connection management, multiplexing, and transport protocols**.

The major versions you should know for web security are:

```
HTTP/0.9
   ↓
HTTP/1.0
   ↓
HTTP/1.1
   ↓
HTTP/2
   ↓
HTTP/3
```

---

## 1. HTTP/0.9

Released around **1991** and extremely primitive.

A request looked like:

```
GET /index.html
```

There were essentially:

- Only `GET`
- No HTTP headers
- No status codes
- No request body
- Response was basically the document itself
- One request per connection

Example:

```
Client ── GET /index.html ──► Server
Client ◄── HTML ────────────── Server
```

### Today

HTTP/0.9 is obsolete and mainly relevant for understanding HTTP's history.

---

# 2. HTTP/1.0

Introduced major improvements.

Example:

```
GET /index.html HTTP/1.0
Host: example.com
```

It introduced/standardized concepts such as:

- HTTP headers
- Status codes
- Different HTTP methods
- Request/response metadata
- Content types
- More structured responses

Example response:

```
HTTP/1.0 200 OK
Content-Type: text/html

<html>
    <h1>Hello</h1>
</html>
```

### Major limitation

Connections were generally closed after a response.

```
Request → Response → Connection closes
Request → Response → Connection closes
Request → Response → Connection closes
```

This created significant overhead for websites containing many resources.

---

# 3. HTTP/1.1

HTTP/1.1 became the dominant version of HTTP for many years and is still widely supported.

Example:

```
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
```

### Major improvements

#### Persistent connections

Multiple requests can use the same TCP connection.

```
TCP Connection
      │
      ├── Request 1 → Response 1
      ├── Request 2 → Response 2
      ├── Request 3 → Response 3
      └── Request 4 → Response 4
```

This reduces connection setup overhead.

---

### Host header

HTTP/1.1 requires the `Host` header.

```
Host: example.com
```

This allows multiple websites to share the same IP address.

For example:

```
203.0.113.10
      │
      ├── example.com
      ├── shop.example.com
      └── another-site.com
```

This concept is very important for **web hosting and virtual hosts**.

---

### Chunked transfer encoding

HTTP/1.1 can send response data in chunks when the complete size isn't known beforehand.

```
Transfer-Encoding: chunked
```

This becomes particularly important when studying **HTTP request smuggling**.

---

### HTTP/1.1 limitations

HTTP/1.1 still has significant performance limitations.

Requests on a connection are fundamentally processed in order.

For example:

```
Request 1 ──────────────►
                         Response 1
Request 2 ──────────────►
                         Response 2
Request 3 ──────────────►
                         Response 3
```

A slow response can contribute to **head-of-line blocking** at the HTTP/1.1 request level.

---

# 4. HTTP/2

HTTP/2 was standardized in **2015**.

Its goal was to make HTTP significantly more efficient without changing the basic web programming model.

A major difference is that HTTP/2 uses a **binary framing layer** rather than HTTP/1.x's textual message framing.

### HTTP/1.1

```
GET /page HTTP/1.1
Host: example.com
...
```

### HTTP/2

The HTTP semantics are still familiar, but they are transmitted using **binary frames**.

---

## Multiplexing

This is one of the biggest improvements.

HTTP/2 can send multiple streams concurrently over a single TCP connection:

```
                 TCP Connection
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
    Stream 1       Stream 2       Stream 3
    /index.html    /style.css     /script.js
        │              │              │
        └──────────────┼──────────────┘
                       ↓
                    Server
```

Instead of waiting for one complete request/response exchange before processing another, frames from multiple streams can be interleaved.

---

## Header compression

HTTP/2 uses **HPACK** to compress HTTP headers.

This reduces the amount of redundant header data transmitted.

For example, browsers repeatedly send headers such as:

```
Cookie: ...
User-Agent: ...
Accept: ...
```

HTTP/2 can efficiently encode repeated header information.

---

## Other HTTP/2 features

Important concepts include:

- Binary framing
- Multiplexing
- Streams
- Stream IDs
- HPACK header compression
- Request prioritization mechanisms
- Server Push (defined in HTTP/2, but later deprecated/removed from common browser use)

---

# 5. HTTP/3

HTTP/3 is the newest major HTTP version.

The biggest architectural difference is its underlying transport.

```
HTTP/1.1 → TCP
HTTP/2   → TCP
HTTP/3   → QUIC → UDP
```

HTTP/3 uses **QUIC**, which runs over UDP.

```
HTTP/3
   ↓
 QUIC
   ↓
 UDP
   ↓
 IP
```

---

## Why QUIC?

TCP has connection-level head-of-line blocking.

HTTP/2 multiplexes streams, but because those streams share a single TCP connection, packet loss can still cause TCP-level blocking.

QUIC is designed to avoid this problem between independent streams.

Conceptually:

```
HTTP/2

TCP connection
      │
      ├── Stream 1
      ├── Stream 2
      └── Stream 3

Packet loss
      ↓
TCP-level impact
```

With QUIC:

```
QUIC connection
      │
      ├── Stream 1
      ├── Stream 2
      └── Stream 3

Loss affecting Stream 1
      ↓
Other streams can continue independently
```

HTTP/3 also incorporates modern transport security using **TLS 1.3** as part of the QUIC protocol stack.


# HTTP Request Line Components

The **request line** is the first line of an HTTP request. It tells the server **what the client wants and which HTTP version it is using**.

For HTTP/1.1, a typical request line is:

```
GET /products?id=123 HTTP/1.1
```

It has **3 main components**:

```
GET          /products?id=123          HTTP/1.1
 │                  │                     │
 │                  │                     │
Method        Request Target          HTTP Version
```

---

## 1. HTTP Method

```
GET
```

The **method** specifies the operation the client wants to perform.

Common methods:

```
GET       → Retrieve data
POST      → Submit/create data
PUT       → Replace data
PATCH     → Partially modify data
DELETE    → Delete data
HEAD      → Retrieve headers
OPTIONS   → Ask about supported options/methods
```

Example:

```
POST /login HTTP/1.1
```

Here, `POST` is the method.

---

# 2. Request Target

Example:

```
GET /products?id=123 HTTP/1.1
    └───────────────┘
      Request Target
```

The **request target** identifies the resource or endpoint the client is requesting.

It can contain:

### Path

```
GET /products HTTP/1.1
```

Path:

```
/products
```

### Path + query string

```
GET /products?id=123&sort=price HTTP/1.1
```

Here:

```
Path          → /products
Query string  → ?id=123&sort=price
```

The query parameters are:

```
id=123
sort=price
```

---

# 3. HTTP Version

Example:

```
GET /products HTTP/1.1
                    └──────┘
                    Version
```

It specifies which HTTP version is being used.

Examples:

```
HTTP/1.0
HTTP/1.1
```

HTTP/2 and HTTP/3 use a different underlying framing mechanism, so you generally won't see a normal textual request line like this on the wire. However, the same HTTP semantics—method, target, headers, etc.—still exist.

# HTTP Headers

These are some of the **most important HTTP headers** you should understand for web development, Burp Suite, and bug bounty.

A header follows this format:

```
Header-Name: value
```

For example:

```
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

---

## 1. `Host`

Specifies the **hostname the client wants to communicate with**.

```
Host: example.com
```

Example:

```
GET /login HTTP/1.1
Host: example.com
```

The server uses the `Host` header to determine which website/application should handle the request.

### Why important?

Multiple websites can share the same IP address:

```
203.0.113.10
     │
     ├── example.com
     ├── shop.example.com
     └── admin.example.com
```

The `Host` header helps the server select the appropriate virtual host.

### Bug bounty relevance

Important when studying:

- Virtual hosts
- Host header attacks
- Web cache poisoning
- Routing behavior
- SSRF-related scenarios

---

# 2. `User-Agent`

Identifies the **client software** making the request.

```
User-Agent: Mozilla/5.0
```

A real browser might send something like:

```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/154.0.0.0 Safari/537.36
```

It can indicate:

```
Browser
Operating system
Browser engine
Client/application
```

### Important

The `User-Agent` is **client-controlled** and therefore should not be trusted for authentication or security decisions.

### Bug bounty relevance

You may modify it to test:

```
Bot detection
Browser-specific behavior
Mobile/desktop behavior
Access-control assumptions
WAF behavior
```

---

# 3. `Accept`

Tells the server what **response media types** the client can handle.

```
Accept: text/html
```

A browser may send:

```
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
```

Examples:

```
Accept: text/html
Accept: application/json
Accept: image/png
Accept: */*
```

`*/*` means:

> Any media type is acceptable.

### Example

```
Accept: application/json
```

The client is essentially saying:

> "I'd prefer a JSON response."

---

# 4. `Accept-Encoding`

Specifies which **content encodings/compression formats** the client supports.

```
Accept-Encoding: gzip, deflate, br
```

Common values:

```
gzip
deflate
br
zstd
```

The server may then respond:

```
Content-Encoding: gzip
```

Meaning the response body has been compressed using gzip.

### Important distinction

```
Accept-Encoding
        ↓
What client supports

Content-Encoding
        ↓
What server actually used
```

---

# 5. `Accept-Language`

Specifies the client's preferred **natural languages**.

```
Accept-Language: en-US,en;q=0.9
```

This means roughly:

```
en-US → preferred
en    → also acceptable
```

A server might use this to return:

```
English
Hindi
French
German
...
```

depending on the application's localization system.

### Bug bounty relevance

Can sometimes matter when testing:

- Language-based behavior
- Localization
- Cache behavior
- Access-control assumptions

---

# 6. `Referer`

Indicates the URL of the page from which the request originated.

Example:

```
Referer: https://example.com/products
```

Suppose you click:

```
/products
     ↓
/checkout
```

The request to `/checkout` might contain:

```
Referer: https://example.com/products
```

### Important

The spelling is historically **`Referer`**, not `Referrer`.

### Security consideration

The `Referer` header can contain information about the previous page and potentially sensitive URL data.

It should generally **not be trusted as an authentication or authorization mechanism** because clients can manipulate headers.

---

# 7. `Origin`

Identifies the **origin** from which a request originated.

Example:

```
Origin: https://example.com
```

An origin consists of:

```
scheme + host + port
```

For example:

```
https://example.com:443
```

is an origin.

`Origin` is particularly important for **CORS** and **CSRF-related behavior**.

Example:

```
POST /api/transfer HTTP/1.1
Host: bank.example
Origin: https://attacker.example
```

The server may use the `Origin` value when deciding whether a cross-origin request should be permitted.

### Important difference

```
Referer
   ↓
Usually contains the referring URL

Origin
   ↓
Contains the requesting origin
```

---

# 8. `Cookie`

Sends cookies previously stored by the browser to the server.

```
Cookie: session=abc123
```

Multiple cookies:

```
Cookie: session=abc123; theme=dark; language=en
```

Cookies can store things such as:

```
Session identifiers
Preferences
Tracking identifiers
Application state
```

### Authentication example

After login, the server might give the browser:

```
Set-Cookie: session=abc123; HttpOnly; Secure
```

The browser subsequently sends:

```
Cookie: session=abc123
```

The server uses the session identifier to associate the request with the logged-in session.

### Bug bounty relevance

Extremely important for:

- Session security
- Authentication
- Session fixation
- Session hijacking
- CSRF
- Cookie security
- Access-control testing

---

# 9. `Authorization`

Carries authentication/authorization credentials.

Common form:

```
Authorization: Bearer eyJhbGciOi...
```

Other schemes exist, such as:

```
Authorization: Basic dXNlcjpwYXNz
```

For a JWT-based application:

```
Authorization: Bearer <JWT>
```

The server can validate the token and determine whether the request is authenticated/authorized.

### Bug bounty relevance

Very important for:

- JWT
- API authentication
- Broken access control
- Token handling
- Authentication bypass
- API security

Never expose real credentials or tokens unnecessarily.

---

# 10. `Content-Type`

Specifies the **media type of the request body**.

Example:

```
Content-Type: application/json
```

with:

```
{
    "username": "john",
    "password": "test123"
}
```

Common values:

### JSON

```
Content-Type: application/json
```

### HTML form

```
Content-Type: application/x-www-form-urlencoded
```

Example body:

```
username=john&password=test123
```

### Multipart form

```
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary
```

Commonly used for file uploads.

### Important distinction

```
Content-Type
      ↓
Type of data being sent
```

Whereas:

```
Accept
      ↓
Type of data the client wants to receive
```

---

# 11. `Content-Length`

Specifies the size of the message body in **bytes**.

Example:

```
Content-Length: 27
```

For:

```
POST /login HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

username=john&password=123
```

The value tells the receiver how many bytes belong to the body.

### Bug bounty relevance

Very important when learning:

- HTTP request parsing
- Proxies
- HTTP/1.1
- Request smuggling

Particularly when studying interactions between:

```
Content-Length
Transfer-Encoding
```

---

# 12. `Connection`

Controls certain aspects of the connection in HTTP/1.x.

Example:

```
Connection: keep-alive
```

This indicates that the TCP connection can be reused for additional requests.

Another value:

```
Connection: close
```

indicates that the connection should be closed after the current request/response.

### Important

`Connection` is primarily relevant to **HTTP/1.x**. HTTP/2 and HTTP/3 handle connection management differently, and `Connection` is not used as a normal end-to-end header there.

---

# 13. `Cache-Control`

Controls caching behavior.

Example:

```
Cache-Control: no-cache
```

Other directives include:

```
Cache-Control: no-store
Cache-Control: private
Cache-Control: public
Cache-Control: max-age=3600
```

### Examples

```
Cache-Control: no-store
```

Means the response should not be stored in a cache.

```
Cache-Control: max-age=3600
```

The response can be considered fresh for 3600 seconds under the applicable caching rules.

### Bug bounty relevance

Important for:

- Web cache behavior
- Cache poisoning
- Sensitive information caching
- Authentication-related caching problems

---

# 14. `If-None-Match`

Used for **conditional requests** with an entity tag (**ETag**).

Suppose the server previously returned:

```
ETag: "abc123"
```

The browser can later send:

```
If-None-Match: "abc123"
```

The server checks whether the resource has changed.

If it hasn't changed:

```
HTTP/1.1 304 Not Modified
```

The browser can use its cached copy.

### Flow

```
First request
     ↓
Server
     ↓
ETag: "abc123"
     ↓
Browser stores it

Later request
     ↓
If-None-Match: "abc123"
     ↓
Server checks resource
     ↓
304 Not Modified
```

---

# 15. `If-Modified-Since`

Another mechanism for **conditional requests**, based on the resource's modification date.

First response:

```
Last-Modified: Sun, 04 Oct 2026 10:00:00 GMT
```

Later request:

```
If-Modified-Since: Sun, 04 Oct 2026 10:00:00 GMT
```

If the resource hasn't changed:

```
HTTP/1.1 304 Not Modified
```

---

# `If-None-Match` vs `If-Modified-Since`

|Header|Based on|
|---|---|
|`If-None-Match`|ETag|
|`If-Modified-Since`|Modification date|

Generally:

```
ETag
 ↓
Specific representation/version identifier

Last-Modified
 ↓
Timestamp
```

# HTTP Security Headers

These are **response headers** that tell the browser how it should handle security-sensitive behavior.

A typical response might contain:

```
HTTP/1.1 200 OK
Content-Security-Policy: default-src 'self'
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=()
Set-Cookie: session=abc123; Secure; HttpOnly; SameSite=Lax
```

Let's understand each.

---

# 1. Content-Security-Policy — `CSP`

**CSP** controls **which resources the browser is allowed to load or execute**.

```
Content-Security-Policy: default-src 'self'
```

This essentially says:

> By default, only load resources from the same origin.

It can control:

- JavaScript
- CSS
- Images
- Fonts
- Frames
- AJAX/fetch connections
- Media
- Plugins and other resource types

### Example

```
Content-Security-Policy: script-src 'self'
```

Means:

> Only allow scripts from the same origin.

A more complex policy:

```
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.example.com; img-src 'self' data:;
```

### Why important for bug bounty?

CSP is particularly relevant to **XSS**.

For example, an application might have an XSS vulnerability, but a strong CSP could make exploitation significantly more difficult.

However:

> **CSP is a security control, not a substitute for fixing XSS.**

### Important directives

```
default-src
script-src
style-src
img-src
font-src
connect-src
frame-src
object-src
base-uri
form-action
frame-ancestors
```

---

# 2. Strict-Transport-Security — `HSTS`

HSTS tells the browser:

> **Always use HTTPS for this website.**

Example:

```
Strict-Transport-Security: max-age=31536000
```

`31536000` seconds = **1 year**.

A stronger configuration might be:

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

### Without HSTS

A user might initially access:

```
http://example.com
```

and potentially be exposed to downgrade/HTTP-related attacks before reaching HTTPS.

### With HSTS

The browser remembers:

```
example.com → HTTPS only
```

and automatically uses HTTPS for future requests.

### Important directives

```
max-age
includeSubDomains
preload
```

### Bug bounty relevance

Important when studying:

- HTTPS
- TLS
- SSL stripping/downgrade attacks
- Transport security

---

# 3. X-Content-Type-Options

Controls whether browsers are allowed to **MIME-sniff** a response.

The common value is:

```
X-Content-Type-Options: nosniff
```

This tells the browser:

> Don't try to guess the content type; respect the declared `Content-Type`.

For example:

```
Content-Type: text/plain
X-Content-Type-Options: nosniff
```

The browser should not decide:

> "This looks like JavaScript, so I'll execute it."

### Why useful?

It helps reduce certain attacks involving incorrectly configured content types, especially where browsers might otherwise interpret content differently than intended.

### Remember

```
Content-Type
      ↓
What the server says the content is

nosniff
      ↓
Browser should not override that interpretation by MIME sniffing
```

---

# 4. X-Frame-Options

Controls whether a page can be loaded inside a `<frame>`, `<iframe>`, `<object>`, etc.

Example:

```
X-Frame-Options: DENY
```

Means:

> Don't allow this page to be framed.

Another value:

```
X-Frame-Options: SAMEORIGIN
```

Means:

> Allow framing only by pages from the same origin.

### Why important?

It helps defend against **clickjacking**.

Imagine a malicious website:

```
<iframe src="https://bank.example/transfer"></iframe>
```

The attacker might attempt to trick the victim into clicking something while the legitimate page is visually hidden or overlaid.

`X-Frame-Options` can prevent the page from being framed.

### Modern alternative

CSP provides:

```
Content-Security-Policy: frame-ancestors 'none'
```

or:

```
Content-Security-Policy: frame-ancestors 'self'
```

`frame-ancestors` is more flexible than `X-Frame-Options`.

---

# 5. Referrer-Policy

Controls **how much referrer information the browser sends** when navigating or making requests.

Example:

```
Referrer-Policy: strict-origin-when-cross-origin
```

Suppose:

```
https://example.com/account/profile
```

links to:

```
https://other.example/
```

The browser might send only:

```
https://example.com/
```

rather than the complete:

```
https://example.com/account/profile
```

### Common policies

```
no-referrer
no-referrer-when-downgrade
origin
origin-when-cross-origin
same-origin
strict-origin
strict-origin-when-cross-origin
unsafe-url
```

### Important security concern

URLs can sometimes contain sensitive information:

```
https://example.com/reset?token=SECRET
```

Sending the complete URL as a referrer could potentially leak the token to another site.

A restrictive `Referrer-Policy` helps reduce this risk.

---

# 6. Permissions-Policy

Controls which **browser features** a website and its embedded content can use.

Example:

```
Permissions-Policy: camera=(), microphone=()
```

This tells the browser to disable camera and microphone access for the relevant origin.

Other browser-controlled features can include:

```
camera
microphone
geolocation
fullscreen
payment
usb
clipboard
```

Example:

```
Permissions-Policy: geolocation=(), camera=(), microphone=()
```

Meaning:

```
Geolocation → disabled
Camera      → disabled
Microphone  → disabled
```

### Why useful?

It reduces the application's exposure to unnecessary browser capabilities.

Think of it as:

> **"This website does not need these browser features, so don't allow them."**

---

# 7. Set-Cookie

`Set-Cookie` is different from the other headers here.

It is used by the **server to tell the browser to create or update a cookie**.

Example:

```
Set-Cookie: session=abc123
```

The browser stores it and may later send:

```
Cookie: session=abc123
```

So:

```
SERVER
   │
   │ Set-Cookie
   ▼
BROWSER
   │
   │ Cookie
   ▼
SERVER
```

---

## Important Cookie Security Attributes

### `Secure`

```
Set-Cookie: session=abc123; Secure
```

The browser should send the cookie only over HTTPS.

---

### `HttpOnly`

```
Set-Cookie: session=abc123; HttpOnly
```

Prevents normal JavaScript from accessing the cookie through `document.cookie`.

This is particularly useful for protecting session cookies against some consequences of XSS.

**Important:** `HttpOnly` does **not** prevent XSS itself.

---

### `SameSite`

Controls when cookies are sent in **cross-site contexts**.

Examples:

```
SameSite=Strict
```

```
SameSite=Lax
```

```
SameSite=None; Secure
```

This is particularly important for understanding **CSRF and cross-site requests**.

---

### `Domain`

Controls which hosts can receive the cookie.

```
Set-Cookie: session=abc123; Domain=example.com
```

---

### `Path`

Controls which URL paths receive the cookie.

```
Set-Cookie: session=abc123; Path=/admin
```

---

### `Max-Age` / `Expires`

Controls cookie lifetime.

```
Set-Cookie: session=abc123; Max-Age=3600
```

---

# Secure Cookie Example

A session cookie might look like:

```
Set-Cookie: session=abc123;
    Secure;
    HttpOnly;
    SameSite=Lax;
    Path=/
```

Conceptually:

```
session=abc123
      │
      ├── Secure
      │     └─ HTTPS only
      │
      ├── HttpOnly
      │     └─ JavaScript can't normally read it
      │
      ├── SameSite=Lax
      │     └─ Restricts some cross-site sending
      │
      └── Path=/
            └─ Available under /
```