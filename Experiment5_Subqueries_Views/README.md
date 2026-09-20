# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage
Table Name: Medications

```sql
SELECT medication_id, medication_name, dosage 
FROM Medications 
WHERE dosage = (SELECT MIN(dosage) FROM Medications);
```

**Output:**

```text
medication_id  medication_name  dosage
-------------  ---------------  ------
2              Ibuprofen        200mg
```

**Question 2**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.
Tables: SALESMAN, ORDERS

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id 
FROM ORDERS 
WHERE salesman_id IN (
    SELECT salesman_id FROM SALESMAN WHERE city = 'New York'
);
```

**Output:**

```text
ord_no  purch_amt  ord_date    customer_id  salesman_id
------  ---------  ----------  -----------  -----------
70001   150.5      2012-10-05  3005         5002
70002   270.65     2012-09-10  3001         5005
```

**Question 3**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.
Sample table: CUSTOMERS

```sql
SELECT * FROM CUSTOMERS WHERE SALARY < 2500;
```

**Output:**

```text
ID  NAME     AGE  ADDRESS    SALARY
--  ----     ---  -------    ------
1   Ramesh   32   Ahmedabad  2000
2   Khilan   25   Delhi      1500
3   Kaushik  23   Kota       2000
```

**Question 4**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.
Sample table: GRADES

```sql
SELECT student_name, grade 
FROM GRADES g1
WHERE grade = (
    SELECT MAX(grade) 
    FROM GRADES g2 
    WHERE g1.subject = g2.subject
);
```

**Output:**

```text
student_name  grade
------------  -----
Charlie       95
Emma          92
John          85
```

**Question 5**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.
SAMPLE TABLE: customer

```sql
SELECT name 
FROM customer 
WHERE phone IN (
    SELECT phone FROM customer GROUP BY phone HAVING COUNT(*) = 1
);
```

**Output:**

```text
name
------------
Aarti Desai
Vivek Sharma
Nisha Patel
Rajesh Singh
Radha Iyer
```

**Question 6**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than 30.
Sample table: CUSTOMERS

```sql
SELECT * FROM CUSTOMERS WHERE AGE < 30;
```

**Output:**

```text
ID  NAME      AGE  ADDRESS    SALARY
--  ----      ---  -------    ------
2   Khilan    25   Delhi      1500
3   Kaushik   23   Kota       2000
4   Chaitali  25   Mumbai     6500
5   Hardik    27   Bhopal     8500
6   Komal     22   Hyderabad  4500
7   Muffy     24   Indore     10000
```

**Question 7**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.
Sample table: CUSTOMERS

```sql
SELECT * FROM CUSTOMERS WHERE SALARY > 4500;
```

**Output:**

```text
ID  NAME      AGE  ADDRESS    SALARY
--  ----      ---  -------    ------
4   Chaitali  25   Mumbai     6500
5   Hardik    27   Bhopal     8500
7   Muffy     24   Indore     10000
```

**Question 8**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi
Sample table: CUSTOMERS

```sql
SELECT * FROM CUSTOMERS WHERE ADDRESS = 'Delhi';
```

**Output:**

```text
ID  NAME    AGE  ADDRESS  SALARY
--  ----    ---  -------  ------
2   Khilan  25   Delhi    1500
```

**Question 9**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.
Sample table: CUSTOMERS

```sql
SELECT * FROM CUSTOMERS WHERE SALARY = 1500;
```

**Output:**

```text
ID  NAME    AGE  ADDRESS  SALARY
--  ----    ---  -------  ------
2   Khilan  25   Delhi    1500
```

**Question 10**
---
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.
customer table

```sql
SELECT grade, COUNT(*) AS count 
FROM customer 
WHERE city = 'New York City' 
  AND grade > (SELECT AVG(grade) FROM customer WHERE city = 'New York City')
GROUP BY grade;
```

**Output:**

```text
grade  count
-----  -----
3      2
```


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
