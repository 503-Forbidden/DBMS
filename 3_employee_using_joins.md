```
CREATE TABLE Employee (
    employee_name VARCHAR2(50) PRIMARY KEY,
    street VARCHAR2(100),
    city VARCHAR2(50)
);
```
```
CREATE TABLE Company (
    company_name VARCHAR2(100) PRIMARY KEY,
    city VARCHAR2(50)
);
```
```
CREATE TABLE Works (
    employee_name VARCHAR2(50),
    company_name VARCHAR2(100),
    salary NUMBER
);
```
```
CREATE TABLE Manages (
    employee_name VARCHAR2(50),
    manager_name VARCHAR2(50)
);
```
```
INSERT INTO Company VALUES ('First Bank Corporation', 'New York');
INSERT INTO Company VALUES ('Small Bank Corporation', 'Chicago');
```
```
INSERT INTO Employee VALUES ('Alice', '123 Main St', 'New York');
INSERT INTO Employee VALUES ('Bob', '456 Oak Ave', 'Chicago');
INSERT INTO Employee VALUES ('Carol', '789 Pine Rd', 'New York');
```
```
INSERT INTO Works VALUES ('Alice', 'First Bank Corporation', 12000);
INSERT INTO Works VALUES ('Bob', 'Small Bank Corporation', 8000);
INSERT INTO Works VALUES ('Carol', 'First Bank Corporation', 9000);
```
```
INSERT INTO Manages VALUES ('Alice', 'Carol');
```
```
SELECT e.employee_name
FROM Employee e
JOIN Works w ON e.employee_name = w.employee_name
WHERE w.company_name = 'First Bank Corporation';
```
```
SELECT e.employee_name, e.city
FROM Employee e
JOIN Works w ON e.employee_name = w.employee_name
WHERE w.company_name = 'First Bank Corporation';
```
```
SELECT e.employee_name, e.street, e.city
FROM Employee e
JOIN Works w ON e.employee_name = w.employee_name
WHERE w.company_name = 'First Bank Corporation'
AND w.salary > 10000;
```
```
SELECT employee_name
FROM Works
WHERE salary > ALL (
    SELECT salary
    FROM Works
    WHERE company_name = 'Small Bank Corporation'
);
```
```
SELECT w.employee_name
FROM Works w
JOIN (
    SELECT company_name, AVG(salary) avg_sal
    FROM Works
    GROUP BY company_name
) avg_w
ON w.company_name = avg_w.company_name
WHERE w.salary > avg_w.avg_sal;
```
```
SELECT company_name
FROM Works
GROUP BY company_name
HAVING SUM(salary) = (
    SELECT MIN(total)
    FROM (
        SELECT SUM(salary) total
        FROM Works
        GROUP BY company_name
    )
);
```
```
SELECT company_name
FROM Works
GROUP BY company_name
HAVING AVG(salary) > (
    SELECT AVG(salary)
    FROM Works
    WHERE company_name = 'First Bank Corporation'
);
```
```
UPDATE Works
SET salary = salary * 1.10
WHERE company_name = 'First Bank Corporation';

COMMIT;
```
```
CREATE TABLE HighEarners AS
SELECT employee_name, salary
FROM Works
WHERE salary > (SELECT AVG(salary) FROM Works);
```
```
DELETE FROM Works
WHERE company_name IN (
    SELECT company_name
    FROM Company
    WHERE city = 'Gotham'
);
```
```
DELETE FROM Employee
WHERE employee_name NOT IN (
    SELECT employee_name FROM Works
);
```
```
COMMIT;
```
