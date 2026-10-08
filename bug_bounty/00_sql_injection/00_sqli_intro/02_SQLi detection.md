
---
SQL injection can occur in **different parts of an SQL query**, not just the `WHERE` clause.

### 1. `WHERE` clause

Common case:

```
SELECT * FROM products WHERE category = '$input'
```

User input is inserted into the filtering condition.

---

### 2. `UPDATE` statement — values

```
UPDATE users
SET email = '$input'
WHERE id = 1
```

The injection occurs in the value being updated.

---

### 3. `UPDATE` statement — `WHERE` clause

```
UPDATE users
SET role = 'user'
WHERE id = '$input'
```

The injection occurs in the condition identifying which rows to update.

---

### 4. `INSERT` statement — values

```
INSERT INTO users (username)
VALUES ('$input')
```

The injection occurs within an inserted value.

---

### 5. `SELECT` — table name

```
SELECT * FROM $input
```

Here the input controls the table name.

---

### 6. `SELECT` — column name

```
SELECT $input FROM users
```

Here the input controls the selected column.

---

### 7. `ORDER BY` clause

```
SELECT * FROM products
ORDER BY $input
```

Here the input controls the sorting expression.



### SQL Injection in Different Contexts

In SQL injection, **context** can mean the way the application receives, processes, or transforms the attacker-controlled input before it reaches the SQL query.

#### 1. URL / Query Parameter

```
GET /products?id=1
```

Input:

```
id=1
```

The value may be inserted into an SQL query.

---

#### 2. Form Data

```
POST /login
Content-Type: application/x-www-form-urlencoded

username=admin&password=test
```

The SQL query may use the submitted form values.

---

#### 3. JSON

```
POST /api/login
Content-Type: application/json

{"username":"admin","password":"test"}
```

The JSON value can become the SQL input.

---

#### 4. XML

```
POST /api/search
Content-Type: application/xml

<search>
    <name>test</name>
</search>
```

The XML value may eventually be incorporated into an SQL query.

---

#### 5. Cookies

```
Cookie: user_id=10
```

If the server uses the cookie value in an SQL query, it can potentially become an SQL injection point.

---

#### 6. HTTP Headers

Some applications use header values in database queries:

```
X-User-ID: 10
```

A header can therefore be an SQL injection entry point if its value reaches a query unsafely.

---

### Encoding and Obfuscation Contexts

Sometimes the application or a security filter transforms the input before it reaches the SQL parser. Common transformations include:

- **URL encoding**
- **Double URL encoding**
- **HTML/XML encoding**
- **JSON escaping**
- **Unicode encoding**
- **Case variation**
- **Whitespace variations**
- **SQL comments**

For example, a character such as:

```
'
```

may be represented in an encoded form and decoded later by the application.