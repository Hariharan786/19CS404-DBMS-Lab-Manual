# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
CREATE TABLE jobs (
  job_id INTEGER PRIMARY KEY,
  job_title TEXT DEFAULT '',
  min_salary REAL DEFAULT 8000,
  max_salary REAL DEFAULT NULL
);
```

**Output:**

```text
cid  name        type     notnull  dflt_value  pk
---  ----------  -------  -------  ----------  --
0    job_id      INTEGER  0                    1 
1    job_title   TEXT     0        ''          0 
2    min_salary  REAL     0        8000        0 
3    max_salary  REAL     0        NULL        0 
```

**Question 2**
---
Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78

```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS) VALUES
(202, 'Ella King', 'F', 'Chemistry', 87),
(203, 'James Bond', 'M', 'Literature', 78);
```

**Output:**

```text
RollNo  Name        Gender  Subject     MARKS
------  ----------  ------  ----------  -----
202     Ella King   F       Chemistry   87   
203     James Bond  M       Literature  78   
```

**Question 3**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.

```sql
INSERT INTO Customers (CustomerID, Name, Address) VALUES
(304, 'Peter Parker', 'Spider St');
```

**Output:**

```text
CustomerID  Name          Address    City     ZipCode
----------  ------------  ---------  -------  -------
304         Peter Parker  Spider St  Chennai  600001 
```

**Question 4**
---
Create a table named Products with the following columns:
ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER

```sql
CREATE TABLE Products (
  ProductID INTEGER,
  ProductName TEXT,
  Price REAL,
  Stock INTEGER
);
```

**Output:**

```text
cid  name         type     notnull  dflt_value  pk
---  -----------  -------  -------  ----------  --
0    ProductID    INTEGER  0                    0 
1    ProductName  TEXT     0                    0 
2    Price        REAL     0                    0 
3    Stock        INTEGER  0                    0 
```

**Question 5**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Invoices (
  InvoiceID INTEGER PRIMARY KEY,
  InvoiceDate DATE,
  Amount REAL CHECK (Amount > 0),
  DueDate DATE CHECK (DueDate > InvoiceDate),
  OrderID INTEGER,
  FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

```text
cid  name         type     notnull  dflt_value  pk
---  -----------  -------  -------  ----------  --
0    InvoiceID    INTEGER  0                    1 
1    InvoiceDate  DATE     0                    0 
2    Amount       REAL     0                    0 
3    DueDate      DATE     0                    0 
4    OrderID      INTEGER  0                    0 
```

**Question 6**
---
Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL

```sql
CREATE TABLE orders (
  ord_id TEXT(4) NOT NULL,
  item_id TEXT NOT NULL,
  ord_date DATE,
  ord_qty INTEGER,
  cost INTEGER,
  PRIMARY KEY (item_id, ord_date)
);
```

**Output:**

```text
cid  name      type     notnull  dflt_value  pk
---  --------  -------  -------  ----------  --
0    ord_id    TEXT(4)  1                    0 
1    item_id   TEXT     1                    1 
2    ord_date  DATE     0                    2 
3    ord_qty   INTEGER  0                    0 
4    cost      INTEGER  0                    0 
```

**Question 7**
---
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.

```sql
ALTER TABLE employee ADD department_id INTEGER;
ALTER TABLE employee ADD manager_id INTEGER DEFAULT NULL;
```

**Output:**

```text
cid  name           type     notnull  dflt_value  pk
---  -------------  -------  -------  ----------  --
0    id             INTEGER  0                    1 
1    name           TEXT     0                    0 
2    department_id  INTEGER  0                    0 
3    manager_id     INTEGER  0        NULL        0 
```

**Question 8**
---
Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0

```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
SELECT RollNo, Name, Gender, Subject, MARKS FROM Archived_students;
```

**Output:**

```text
RollNo  Name         Gender  Subject  MARKS
------  -----------  ------  -------  -----
204     Alice Smith  F       Math     90   
```

**Question 9**
---
Write an SQL query to change the name of the column id to employee_id in the table employee.

```sql
ALTER TABLE employee RENAME COLUMN id TO employee_id;
```

**Output:**

```text
cid  name           type     notnull  dflt_value  pk
---  -------------  -------  -------  ----------  --
0    employee_id    INTEGER  0                    1 
1    name           TEXT     0                    0 
2    department_id  INTEGER  0                    0 
3    manager_id     INTEGER  0        NULL        0 
```

**Question 10**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments (
  AssignmentID INTEGER PRIMARY KEY,
  EmployeeID INTEGER,
  ProjectID INTEGER,
  AssignmentDate DATE NOT NULL,
  FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
  FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

```text
cid  name            type     notnull  dflt_value  pk
---  --------------  -------  -------  ----------  --
0    AssignmentID    INTEGER  0                    1 
1    EmployeeID      INTEGER  0                    0 
2    ProjectID       INTEGER  0                    0 
3    AssignmentDate  DATE     1                    0 
```


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
