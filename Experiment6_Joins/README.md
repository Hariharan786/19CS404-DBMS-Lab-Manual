# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column.

```sql
SELECT c.cust_name, o.ord_no, o.ord_date, o.purch_amt
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id;
```

**Output:**

```text
cust_name       ord_no  ord_date    purch_amt
--------------  ------  ----------  ---------
Nick Rimando    70002   2012-10-05  65.26
Nick Rimando    70008   2012-09-10  5760.0
Brad Davis      70005   2012-07-27  2400.6
Graham Zusi     70001   2012-10-05  150.5
Graham Zusi     70007   2012-09-10  948.5
Julian Green    70012   2012-06-27  250.45
Fabian Johnson  70010   2012-10-10  1983.43
Geoff Cameron   70004   2012-08-17  110.5
Geoff Cameron   70003   2012-10-10  2480.4
Jozy Altidor    70011   2012-08-17  75.29
Brad Guzan      70009   2012-09-10  270.65
```

**Question 2**
---
Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

```sql
SELECT p.first_name, p.last_name
FROM patients p
INNER JOIN surgeries s ON p.patient_id = s.patient_id
WHERE s.surgery_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**

```text
first_name  last_name
----------  ---------
Alice       Williams
```

**Question 3**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'London'.

```sql
SELECT s.name
FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id
WHERE c.city = 'London';
```

**Output:**

```text
name
----------
Nail Knite
Pit Alex
```

**Question 4**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.

```sql
SELECT p.first_name, s.*
FROM patients p
INNER JOIN surgeries s ON p.patient_id = s.patient_id
WHERE (p.discharge_date BETWEEN '2024-03-01' AND '2024-03-31')
  AND (p.admission_date NOT BETWEEN '2024-03-01' AND '2024-03-31');
```

**Output:**

```text
first_name  surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ----------  ------------
Bob         102         2           5           2024-02-18
```

**Question 5**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.

```sql
SELECT c.cust_name, c.city AS customer_city, c.grade, s.name AS salesman, s.city AS salesman_city
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;
```

**Output:**

```text
cust_name       customer_city  grade  salesman    salesman_city
--------------  -------------  -----  ----------  -------------
Brad Guzan      London                Pit Alex    London
Nick Rimando    New York       100    James Hoog  New York
Jozy Altidor    Moscow         200    Paul Adam   Rome
Fabian Johnson  Paris          300    Mc Lyon     Paris
Graham Zusi     California     200    Nail Knite  Paris
Brad Davis      New York       200    James Hoog  New York
Julian Green    London         300    Nail Knite  Paris
Geoff Cameron   Berlin         100    Lauson Hen  San Jose
```

**Question 6**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

```sql
SELECT c.cust_name, c.city, o.ord_no, o.ord_date, o.purch_amt, s.name AS salesperson, s.commission
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
LEFT JOIN salesman s ON c.salesman_id = s.salesman_id;
```

**Output:**

```text
cust_name       city        ord_no  ord_date    purch_amt  salesperson  commission
--------------  ----------  ------  ----------  ---------  -----------  ----------
Nick Rimando    New York    70002   2012-10-05  65.26      James Hoog   0.15
Nick Rimando    New York    70008   2012-09-10  5760.0     James Hoog   0.15
Brad Davis      New York    70005   2012-07-27  2400.6     James Hoog   0.15
Graham Zusi     California  70001   2012-10-05  150.5      Nail Knite   0.13
...
```

**Question 7**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id.

```sql
SELECT c.cust_name, c.city AS customer_city, c.grade, s.name AS Salesman, s.city AS salesmancity
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE c.grade < 300
ORDER BY c.customer_id ASC;
```

**Output:**

```text
cust_name      customer_city  grade  Salesman    salesmancity
-------------  -------------  -----  ----------  ------------
Nick Rimando   New York       100    James Hoog  New York
Jozy Altidor   Moscow         200    Paul Adam   Rome
Graham Zusi    California     200    Nail Knite  Paris
Brad Davis     New York       200    James Hoog  New York
Geoff Cameron  Berlin         100    Lauson Hen  San Jose
```

**Question 8**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned.

```sql
SELECT * 
FROM orders 
JOIN customer USING (customer_id) 
JOIN salesman USING (salesman_id);
```

**Output:**

```text
salesman_id  customer_id  ord_no  purch_amt  ord_date    cust_name     city        grade  name        city        commission
-----------  -----------  ------  ---------  ----------  ------------  ----------  -----  ----------  ----------  ----------
5002         3005         70001   150.5      2012-10-05  Graham Zusi   California  200    Nail Knite  Paris       0.13
5005         3001         70009   270.65     2012-09-10  Brad Guzan    London             Pit Alex    London      0.11
5001         3002         70002   65.26      2012-10-05  Nick Rimando  New York    100    James Hoog  New York    0.15
...
```

**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column.

```sql
SELECT p.first_name AS patient_name, a.*
FROM patients p
INNER JOIN appointments a ON p.patient_id = a.patient_id;
```

**Output:**

```text
patient_name  appointment_id  patient_id  doctor_id  appointment_date
------------  --------------  ----------  ---------  -------------------
Alice         1               1           1          2024-01-05 10:00:00
Bob           2               2           2          2024-02-20 14:30:00
Charlie       3               3           3          2024-03-15 09:15:00
```

**Question 10**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

```sql
SELECT o.ord_no, o.purch_amt, c.cust_name, c.city
FROM orders o
JOIN customer c ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**

```text
ord_no  purch_amt  cust_name       city
------  ---------  --------------  ----------
70007   948.5      Graham Zusi     California
70010   1983.43    Fabian Johnson  Paris
```


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
