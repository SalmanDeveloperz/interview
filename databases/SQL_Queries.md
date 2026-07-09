# SQL Notes – Basic Database Commands

A quick revision guide for commonly used SQL commands with examples.

---

# 1. SELECT

The `SELECT` statement is used to retrieve one or more columns from a table.

## Syntax

```sql
SELECT column1, column2
FROM table_name;
```

### Select All Columns

```sql
SELECT *
FROM customers;
```

### Select Specific Columns

```sql
SELECT first_name, last_name, points
FROM customers;
```

---

# 2. FROM

The `FROM` clause specifies which table the data should be retrieved from.

```sql
SELECT *
FROM orders;
```

---

# 3. WHERE

The `WHERE` clause filters rows based on a condition.

## Comparison Operators

| Operator | Meaning |
|----------|---------|
| = | Equal to |
| != or <> | Not equal to |
| < | Less than |
| <= | Less than or equal |
| > | Greater than |
| >= | Greater than or equal |

## Logical Operators

- `AND`
- `OR`
- `NOT`

### Example

```sql
USE sql_store;

SELECT *
FROM order_items
WHERE order_id = 6
AND (unit_price * quantity) > 30;
```

Another example:

```sql
SELECT *
FROM customers
WHERE points > 3000
AND state = 'VA';
```

---

# 4. IN

The `IN` operator is used when checking multiple possible values.

Instead of writing:

```sql
WHERE quantity_in_stock = 49
   OR quantity_in_stock = 38
   OR quantity_in_stock = 72;
```

Use:

```sql
USE sql_store;

SELECT *
FROM products
WHERE quantity_in_stock IN (49, 38, 72);
```

It can also be used with strings:

```sql
SELECT *
FROM customers
WHERE state IN ('VA', 'TX', 'FL');
```

---

# 5. BETWEEN

The `BETWEEN` operator checks whether a value falls within a given range (inclusive).

Instead of:

```sql
WHERE points >= 1000
AND points <= 3000;
```

Use:

```sql
SELECT *
FROM customers
WHERE points BETWEEN 1000 AND 3000;
```

Another example:

```sql
SELECT *
FROM products
WHERE unit_price BETWEEN 10 AND 50;
```

---

# 6. LIKE

The `LIKE` operator is used for pattern matching.

## Wildcards

| Wildcard | Meaning |
|----------|---------|
| `%` | Any number of characters |
| `_` | Exactly one character |

## Examples

### Contains "a"

```sql
SELECT *
FROM customers
WHERE first_name LIKE '%a%';
```

### Starts with "A"

```sql
SELECT *
FROM customers
WHERE first_name LIKE 'A%';
```

### Ends with "a"

```sql
SELECT *
FROM customers
WHERE first_name LIKE '%a';
```

### Second letter is "a"

```sql
SELECT *
FROM customers
WHERE first_name LIKE '_a%';
```

### Phone Number Examples

Ends with 9

```sql
SELECT *
FROM customers
WHERE phone LIKE '%9';
```

11-digit number ending with 9

```sql
SELECT *
FROM customers
WHERE phone LIKE '__________9';
```

---

# 7. REGEXP

`REGEXP` (Regular Expressions) provides more powerful pattern matching than `LIKE`.

## Basic Search

```sql
SELECT *
FROM customers
WHERE address REGEXP 'TRAIL';
```

## Special Characters

| Symbol | Meaning |
|---------|----------|
| ^ | Beginning of string |
| $ | End of string |
| \| | OR |
| [] | Match any character inside brackets |
| [a-z] | Character range |

---

## Starts With

```sql
SELECT *
FROM customers
WHERE address REGEXP '^TRAIL';
```

---

## Ends With

```sql
SELECT *
FROM customers
WHERE address REGEXP 'TRAIL$';
```

---

## Multiple Patterns (OR)

```sql
SELECT *
FROM customers
WHERE state REGEXP 'VA|CO|TX|IL';
```

---

## Character Matching

Matches names containing:

- aa
- ea
- ia

```sql
SELECT *
FROM customers
WHERE last_name REGEXP '[aei]a';
```

---

## Character Range

```sql
SELECT *
FROM customers
WHERE last_name REGEXP '[a-h]';
```

---

## Practice Examples

### First names are ELKA or AMBUR

```sql
SELECT *
FROM customers
WHERE first_name REGEXP 'ELKA|AMBUR';
```

### Last names end with EY or ON

```sql
SELECT *
FROM customers
WHERE last_name REGEXP 'EY$|ON$';
```

### Last names start with MY or contain SE

```sql
SELECT *
FROM customers
WHERE last_name REGEXP '^MY|SE';
```

### Last names contain BR or BU

```sql
SELECT *
FROM customers
WHERE last_name REGEXP 'BR|BU';
```

---

# 8. IS NULL

Used to find rows where a column has no value (`NULL`).

### Customers without phone numbers

```sql
SELECT *
FROM customers
WHERE phone IS NULL;
```

### Orders that haven't been shipped

```sql
SELECT *
FROM orders
WHERE shipped_date IS NULL;
```

### Opposite Condition

```sql
SELECT *
FROM customers
WHERE phone IS NOT NULL;
```

---

# 9. ORDER BY

Used to sort the result set.

Default order is **Ascending (ASC)**.

## Ascending Order

```sql
SELECT *
FROM customers
ORDER BY first_name;
```

---

## Descending Order

```sql
SELECT *
FROM customers
ORDER BY first_name DESC;
```

---

## Sort by Calculated Column

```sql
SELECT *,
       quantity * unit_price AS total_price
FROM order_items
WHERE order_id = 2
ORDER BY total_price DESC;
```

---

## Multiple Columns

```sql
SELECT *
FROM customers
ORDER BY state ASC,
         points DESC;
```

---

# 10. LIMIT

The `LIMIT` clause restricts the number of rows returned.

## First 5 Rows

```sql
SELECT *
FROM customers
LIMIT 5;
```

---

## Top 3 Loyal Customers

```sql
SELECT *
FROM customers
ORDER BY points DESC
LIMIT 3;
```

---

## Pagination

Skip first 6 rows and return next 3.

```sql
SELECT *
FROM customers
LIMIT 6, 3;
```

Equivalent syntax (supported in PostgreSQL):

```sql
SELECT *
FROM customers
LIMIT 3 OFFSET 6;
```

---

# Quick Summary

| Command | Purpose |
|----------|---------|
| `SELECT` | Retrieve data from a table |
| `FROM` | Specify the source table |
| `WHERE` | Filter rows |
| `IN` | Match multiple values |
| `BETWEEN` | Match a range of values |
| `LIKE` | Pattern matching using `%` and `_` |
| `REGEXP` | Advanced pattern matching |
| `IS NULL` | Check for NULL values |
| `ORDER BY` | Sort results |
| `LIMIT` | Restrict number of rows returned |

---

# Example Query

```sql
USE sql_store;

SELECT
    first_name,
    last_name,
    points
FROM customers
WHERE points BETWEEN 1000 AND 3000
    AND state IN ('VA', 'TX')
ORDER BY points DESC
LIMIT 5;
```

This query:

- Selects customers from the `customers` table.
- Retrieves `first_name`, `last_name`, and `points`.
- Filters customers with points between **1000** and **3000**.
- Includes only customers from **VA** or **TX**.
- Sorts by points in descending order.
- Returns only the top **5** matching records.

---
