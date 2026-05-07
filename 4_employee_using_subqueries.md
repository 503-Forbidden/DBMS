```
SELECT employee_name
FROM Works
WHERE company_name = 'First Bank Corporation';
```
```
SELECT employee_name, city
FROM Employee
WHERE employee_name IN (
SELECT employee_name
FROM Works
WHERE company_name = 'First Bank Corporation'
);
```
```
SELECT employee_name, street, city
FROM Employee
WHERE employee_name IN (
    SELECT employee_name
    FROM Works
    WHERE company_name = 'First Bank Corporation'
    AND salary > 10000
);
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
SELECT employee_name
FROM Works w1
WHERE salary > (
SELECT AVG(salary)
FROM Works w2
WHERE w2.company_name = w1.company_name
);
```
```
SELECT company_name
FROM Works
GROUP BY company_name
HAVING SUM(salary) = (
SELECT MIN(total_pay)
FROM (
SELECT SUM(salary) AS total_pay
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
INSERT INTO HighEarners (employee_name, salary)
SELECT employee_name, salary
FROM Works
WHERE salary > (SELECT AVG(salary) FROM Works);
COMMIT;
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
