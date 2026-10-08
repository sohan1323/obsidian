
---
### SQLi Example — Retrieving Hidden Data

Suppose an application has:

```
GET /products?category=Gifts
```

The server constructs:

```
SELECT * FROM products
WHERE category = 'Gifts'
AND released = 1;
```

The application normally shows only **released** products.

An attacker modifies the `category` parameter:

```
Gifts' OR 1=1--
```

The resulting query becomes conceptually:

```
SELECT * FROM products
WHERE category = 'Gifts' OR 1=1--'
AND released = 1;
```

Because:

```
1=1
```

is always true, the query can return **all products**, including products that were intended to remain hidden.

**Impact:** SQL injection allows the attacker to bypass the application's filtering condition and retrieve data that should not be displayed.