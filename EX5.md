# Ex. No: 5 Creating Triggers using PL/SQL
### DATE:
### AIM:
To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
```
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000);
```
### Create employee table

![image](https://github.com/svarsha220/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/127709117/8d2c0d8a-a4d4-435e-9282-905923cf0622)

### Create salary_log table

![image](https://github.com/svarsha220/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/127709117/1e97037a-d4f0-40f7-9c57-0229abbb8a89)

### PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000);

-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;
```

### Output:

![image](https://github.com/svarsha220/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/127709117/f3e4536c-834f-4ed9-bced-99d19372b10c)

![image](https://github.com/svarsha220/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/127709117/4858f24c-4e36-4f3d-bf64-af7c1b3f3079)

### Result:

The program has been implemented successfully..

