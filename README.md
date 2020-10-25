# Payroll-Service-Database
## UC-1-AbilityToCreateAPayrollServiceDatabase
### Create database
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
### Create Table with unique id as primary key, name, salary and start_date as fields
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

### View Table Description
```
DESCRIBE employee_payroll;
```

## UC-3-CreateEmployeePayrollData
### Insert Payroll Data into Table
```
INSERT INTO employee_payroll (name,salary,start_date) VALUES
('Bill',1000000.00,'2018-01-03'),
('Terisa',2000000.00,'2019-11-13'),
('Charlie',3000000.00,'2020-05-21');
```