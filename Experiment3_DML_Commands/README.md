# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

**Question 1**
--
Write a SQL statement to Update the product_name to 'Premium Bread' whose product ID is 5 in the products table.

```sql
UPDATE products SET product_name = 'Premium Bread' WHERE product_id = 5;
```

**Output:**

```text
Rows affected: 1
```

**Question 2**
---
Write a SQL statement to Increase the selling price per unit by 5% for product ID 15 who's sale is on '2023-01-31'.

```sql
UPDATE sales SET sell_price = sell_price * 1.05 WHERE product_id = 15 AND sale_date = '2023-01-31';
```

**Output:**

```text
Rows affected: 1
```

**Question 3**
---
Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

```sql
UPDATE products SET reorder_lvl = reorder_lvl * 0.70 WHERE cost_price > 50 AND quantity < 100;
```

**Output:**

```text
Rows affected: 1
```

**Question 4**
---
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

```sql
UPDATE products SET reorder_lvl = 20 WHERE quantity < 10 AND category = 'Snacks';
```

**Output:**

```text
Rows affected: 1
```

**Question 5**
---
Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

```sql
UPDATE products SET sell_price = sell_price * 1.15 WHERE quantity < 50 AND supplier_id = 10;
```

**Output:**

```text
Rows affected: 1
```

**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

```sql
DELETE FROM customer WHERE GRADE < 2;
```

**Output:**

```text
Rows affected: 1
```

**Question 7**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -
'cust_city' should begin with the letter 'L'.

```sql
DELETE FROM customer WHERE cust_city LIKE 'L%';
```

**Output:**

```text
Rows affected: 1
```

**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'OPENING_AMT' is between 4000 and 6000.

```sql
DELETE FROM customer WHERE OPENING_AMT BETWEEN 4000 AND 6000;
```

**Output:**

```text
Rows affected: 1
```

**Question 9**
---
Write a SQL query to Delete customers from 'customer' table where 'AGENT_CODE' is either 'A003' or 'A008'.

```sql
DELETE FROM customer WHERE AGENT_CODE IN ('A003', 'A008');
```

**Output:**

```text
Rows affected: 1
```

**Question 10**
---
Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

```sql
DELETE FROM Doctors WHERE doctor_id = 1;
```

**Output:**

```text
Rows affected: 1
```

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
