# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

### **Question 1: Write a PL/SQL Procedure to Find the Square of a Number**

**Task: Create a procedure named find_square that accepts a number as input, computes its square, and displays the result. Call the procedure with 6.**

### Code
```sql
CREATE OR REPLACE PROCEDURE find_square(
    p_num IN NUMBER
)
IS
    v_square NUMBER;
BEGIN
    v_square := p_num * p_num;
    DBMS_OUTPUT.PUT_LINE(
        'Square of ' || p_num || ' is ' || v_square
    );
END;
/
BEGIN
    find_square(6);
END;
/
```

### Output
![output](images/output1.png)

---

### **Question 2: Write a PL/SQL Function to Return the Factorial of a Number**

**Task: Create a function named get_factorial that accepts a number, uses a loop to calculate its factorial, and returns the result. Call the function for 5.**

### Code
```sql
CREATE OR REPLACE FUNCTION get_factorial(
    p_num IN NUMBER
)
RETURN NUMBER
IS
    v_factorial NUMBER := 1;
BEGIN
    FOR i IN 1..p_num LOOP
        v_factorial := v_factorial * i;
    END LOOP;
    RETURN v_factorial;
END;
/
DECLARE
    v_num NUMBER := 5;
    v_result NUMBER;
BEGIN
    v_result := get_factorial(v_num);
    DBMS_OUTPUT.PUT_LINE(
        'Factorial of ' || v_num || ' is ' || v_result
    );
END;
/
```

### Output
![output](images/output2.png)

---

### **Question 3: Write a PL/SQL Procedure to Check Whether a Number is Even or Odd**

**Task: Create a procedure named check_even_odd that uses the MOD function to determine whether a number is divisible by 2. Call the procedure with 12.**

### Code
```sql
CREATE OR REPLACE PROCEDURE check_even_odd(
    p_num IN NUMBER
)
IS
BEGIN
    IF MOD(p_num, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(p_num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(p_num || ' is Odd');
    END IF;
END;
/
BEGIN
    check_even_odd(12);
END;
/
```

### Output
![output](images/output3.png)

---

### **Question 4: Write a PL/SQL Function to Return the Reverse of a Number**

**Task: Create a function named reverse_number that reverses the digits of an input number using a loop and returns the reversed number. Call the function with 1234.**

### Code
```sql
CREATE OR REPLACE FUNCTION reverse_number(
    p_num IN NUMBER
)
RETURN NUMBER
IS
    v_num NUMBER := p_num;
    v_reverse NUMBER := 0;
    v_digit NUMBER;
BEGIN
    WHILE v_num > 0 LOOP
        v_digit := MOD(v_num, 10);
        v_reverse := v_reverse * 10 + v_digit;
        v_num := TRUNC(v_num / 10);
    END LOOP;
    RETURN v_reverse;
END;
/
DECLARE
    v_num NUMBER := 1234;
    v_result NUMBER;
BEGIN
    v_result := reverse_number(v_num);
    DBMS_OUTPUT.PUT_LINE(
        'Reversed number of ' || v_num || ' is ' || v_result
    );
END;
/
```

### Output
![output](images/output4.png)

---

### **Question 5: Write a PL/SQL Procedure to Display the Multiplication Table of a Number**

**Task: Create a procedure named print_table that uses a loop from 1 to 10 to display the multiplication table of an input number. Call the procedure with 5.**

### Code
```sql
CREATE OR REPLACE PROCEDURE print_table(
    p_num IN NUMBER
)
IS
BEGIN
    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(
            p_num || ' x ' || i || ' = ' || (p_num * i)
        );
    END LOOP;
END;
/
BEGIN
    print_table(5);
END;
/
```

### Output
![output](images/output5.png)

---

## RESULT
Thus, the PL/SQL programs using procedures and functions were successfully written, compiled, and executed. The required concepts of calculations, decision-making, looping, procedures, and functions were implemented with appropriate output.
