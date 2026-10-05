
---
# SQL Injection in XML Input allows Filter Bypass and Database Query Manipulation

## 1. Executive Summary

A SQL injection vulnerability exists in an XML-based product search/filter functionality where user-controlled XML input is incorporated into a backend SQL query. The application attempts to block SQL injection using a keyword-based input filter, but the filter can be bypassed by encoding SQL characters using XML entities, allowing malicious SQL syntax to reach the database and alter the application's query logic.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection (SQLi) — Filter Bypass via XML Encoding
    
- **Target Endpoint/URL:** `/product/stock`
    
- **Affected Parameter(s):** `storeId` within the XML request body
    
- **Authentication Level Required:** Unauthenticated
    

The application accepts XML input containing a `storeId` value and uses this value in a SQL query.

The application attempts to prevent SQL injection by detecting malicious characters or SQL syntax before processing the request. However, because XML entities are decoded by the XML parser before the value reaches the SQL layer, characters such as a single quote can be represented using XML encoding.

For example:

```
&#39;
```

is decoded to:

```
'
```

This allows the SQL injection payload to bypass the application's input filter.

## 3. Steps to Reproduce (STR)

1. Access the PortSwigger lab.
    
2. Navigate to the product/stock functionality.
    
3. Intercept the request using Burp Suite.
    
4. Observe that the application sends an XML request containing a `storeId` value.
    
5. Test whether the input is vulnerable to SQL injection by modifying the `storeId` value.
    
6. Observe that a conventional SQL injection payload is blocked by the application's input filter.
    
7. Encode the SQL metacharacters using XML entities.
    
8. For example, represent a single quote as:
    

```
&#39;
```

9. Modify the `storeId` parameter to an XML-encoded SQL injection payload such as:
    

```
1&#39; OR 1=1--
```

10. Send the modified request.
    
11. The XML parser decodes `&#39;` into `'` before the value reaches the SQL query.
    
12. The resulting SQL syntax is therefore effectively equivalent to:
    

```
1' OR 1=1--
```

13. Observe that the SQL injection succeeds despite the application's input filter.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

```
POST /product/stock HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Content-Type: application/xml
Content-Length: <length>

<?xml version="1.0" encoding="UTF-8"?>
<stockCheck>
    <productId>1</productId>
    <storeId>1&#39; OR 1=1--</storeId>
</stockCheck>
```

The XML parser converts:

```
&#39;
```

to:

```
'
```

before the value is processed by the database layer.

The backend therefore effectively receives:

```
1' OR 1=1--
```

which can alter the intended SQL query.

```
HTTP/1.1 200 OK
Content-Type: application/xml

<stockCheckResponse>
    ...
</stockCheckResponse>
```

The successful response demonstrates that the SQL injection payload passed through the application's filtering mechanism.

### Evidence (Screenshots/Video)



## 5. Impact Analysis

- **Technical Impact:** An attacker can bypass the application's SQL injection filter by representing SQL metacharacters as XML entities. Once the XML parser decodes the entities, the resulting characters can be interpreted as SQL syntax, allowing the attacker to manipulate the backend SQL query.
    
- **Business Impact:** Successful exploitation can potentially expose or manipulate database information, depending on the privileges of the application's database account and the SQL query being targeted. In this lab, the primary demonstrated impact is bypassing the application's input filter and achieving SQL injection.
    

## 6. Remediation & References

- **Suggested Fix:** Do not rely on blacklist-based filtering to prevent SQL injection. Use parameterized queries/prepared statements so that decoded XML input is always treated as data rather than executable SQL.
    

For example:

```
cursor.execute(
    "SELECT stock FROM products WHERE product_id = %s AND store_id = %s",
    (product_id, store_id)
)
```

Additionally:

- Parse and canonicalize XML input before performing validation.
    
- Perform validation on the normalized/decoded representation.
    
- Avoid blacklisting individual SQL keywords or characters as the primary security control.
    
- Apply least-privilege permissions to the application's database account.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection