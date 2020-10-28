# Payroll-Service-Database
## UC-1-AbilityToCreateAPayrollServiceDatabase
### To create database
```
CREATE DATABASE payroll_service;
```

### To see the list of all databases
```
SHOW DATABASES;
```

### To use payroll_service database
```
USE payroll_service;
```

### To see current database
```
SELECT DATABASE();
```

## UC-2-CreateAndManageEmployeePayrollTable
### To create Table with unique id as primary key, name, salary and start_date as fields
```
CREATE TABLE employee_payroll
(
id INT unsigned NOT NULL AUTO_INCREMENT,
name VARCHAR(150) NOT NULL,
salary Double NOT NULL,
start_date DATE NOT NULL,
PRIMARY KEY (id)
);
```

### To view Table Description
```
DESCRIBE employee_payroll;
```

## UC-3-CreateEmployeePayrollData
### To insert Payroll Data into Table
```
INSERT INTO employee_payroll (name,salary,start_date) VALUES
('Bill',1000000.00,'2018-01-03'),
('Terisa',2000000.00,'2019-11-13'),
('Charlie',3000000.00,'2020-05-21');
```

## UC-4-RetrieveDataFromDatabase
### To retrieve all records from table
```
SELECT * FROM employee_payroll;
```

## UC-5-RetrieveDataFromAParticularEmployee
### To view Bill Entry
```
SELECT salary FROM employee_payroll WHERE name='Bill';
```

### To view all employees who joined in the given date range
```
SELECT * FROM employee_payroll WHERE start_date BETWEEN CAST('2018-01-01' AS DATE) AND DATE(NOW());
```

## UC-6-AddNewColumnToTableAndUpdateTheRows
### To add gender field
```
ALTER TABLE employee_payroll ADD gender CHAR(1) AFTER name;
```

### To set all male employees' gender to M and female employees' gender to F
```
UPDATE employee_payroll SET gender='M' WHERE name='Bill' or name='Charlie';
UPDATE employee_payroll SET gender='F' WHERE name='Terisa';
```

## UC-7-UsingGroupByToAnalyzeData
### To do analysis by using database functions like sum, avg, min, max, count
```
SELECT gender,SUM(salary) FROM employee_payroll GROUP BY gender;
SELECT gender,AVG(salary) FROM employee_payroll GROUP BY gender;
SELECT gender,MIN(salary) FROM employee_payroll GROUP BY gender;
SELECT gender,MAX(salary) FROM employee_payroll GROUP BY gender;
SELECT gender,COUNT(name) FROM employee_payroll GROUP BY gender;
```

## UC-8-AddPhoneNoAddressAndDepartmentFields
### To add phone_number,address with default and department with not-null as fields
```
ALTER TABLE employee_payroll ADD phone_number VARCHAR(25) AFTER name;
ALTER TABLE employee_payroll ADD address VARCHAR(250) AFTER phone_number;
ALTER TABLE employee_payroll ADD department VARCHAR(150) NOT NULL AFTER address;
ALTER TABLE employee_payroll ALTER address SET DEFAULT 'TBD';
```

## UC-9-AddEmployeePayrollRelatedFields
### To add basic_pay(rename salary to basic_pay), deductions, taxable_pay, income_tax and net_pay fields
```
ALTER TABLE employee_payroll RENAME COLUMN salary TO basic_pay;
ALTER TABLE employee_payroll ADD deductions Double NOT NULL AFTER basic_pay;
ALTER TABLE employee_payroll ADD taxable_pay Double NOT NULL AFTER deductions;
ALTER TABLE employee_payroll ADD tax Double NOT NULL AFTER taxable_pay;
ALTER TABLE employee_payroll ADD net_pay Double NOT NULL AFTER tax;
```

## UC-10.1-AddTerisaToBothSalesAndMarketingDepartments
### To add the employee named 'Terisa' to both Sales and Marketing departments
```
UPDATE employee_payroll SET department='Sales' where name='Terisa';
INSERT INTO employee_payroll (name, department, gender, basic_pay, deductions, taxable_pay, tax, net_pay, start_date) VALUES ('Terisa','Marketing','F',3000000.00,1000000.00,2000000.00,500000.00,1500000.00,'2019-11-13');
```