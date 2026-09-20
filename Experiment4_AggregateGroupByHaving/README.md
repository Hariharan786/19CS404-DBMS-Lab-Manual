# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
What is the count of male and female patients?
Sample table: Patients Table

```sql
SELECT Gender, COUNT(*) AS TotalPatients 
FROM Patients 
GROUP BY Gender;
```

**Output:**

```text
Gender   TotalPatients
------   -------------
Female   5
Male     5
```

**Question 2**
---
How many patients are there in each age group category (e.g., under 20, 20-30, 30-40, etc.)?
Sample table: Patients Table

```sql
SELECT 
  CASE 
    WHEN (strftime('%Y', 'now') - strftime('%Y', DateOfBirth)) < 20 THEN 'under 20'
    WHEN (strftime('%Y', 'now') - strftime('%Y', DateOfBirth)) BETWEEN 20 AND 30 THEN '20-30'
    WHEN (strftime('%Y', 'now') - strftime('%Y', DateOfBirth)) BETWEEN 31 AND 40 THEN '31-40'
    WHEN (strftime('%Y', 'now') - strftime('%Y', DateOfBirth)) BETWEEN 41 AND 50 THEN '41-50'
    ELSE 'Above 50'
  END AS AgeGroup,
  COUNT(*) AS TotalPatients
FROM Patients
GROUP BY AgeGroup;
```

**Output:**

```text
AgeGroup   TotalPatients
--------   -------------
20-30      1
31-40      5
41-50      3
Above 50   1
```

**Question 3**
---
How many doctors specialize in each medical specialty?
Sample table: Doctors Table

```sql
SELECT Specialty, COUNT(*) AS TotalDoctors 
FROM Doctors 
GROUP BY Specialty;
```

**Output:**

```text
Specialty         TotalDoctors
---------         ------------
Gastroenterology  1
Neurology         1
Obstetrics        3
Ophthalmology     1
Orthopedics       1
Pediatrics        2
Urology           1
```

**Question 4**
---
Write a SQL query to find the customer with longest name?
Table: customer

```sql
SELECT name, LENGTH(name) AS length 
FROM customer 
ORDER BY length DESC 
LIMIT 1;
```

**Output:**

```text
name          length
----          ------
Preeti Patel  12
```

**Question 5**
---
Write a SQL query to find the youngest employee in the company?
Table: employee

```sql
SELECT name AS Employee_Name, age AS Age 
FROM employee 
WHERE age = (SELECT MIN(age) FROM employee);
```

**Output:**

```text
Employee_Name   Age
-------------   ---
Peter           32
```


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
