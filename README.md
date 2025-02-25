# mysql

Q1

Retrieve unique job titles from the "employees" table.

SELECT DISTINCT job_title FROM employees;


Q2

Retrieve employees hired in the last 6 months.
SELECT * FROM employees WHERE hire_date >= NOW() - INTERVAL 6 MONTH;


Q3

Get a list of employees with their department names.

SELECT e.name, d.department_name  
FROM employees e  
JOIN departments d ON e.department_id = d.id;


q4

Find employees who do not belong to any department.

SELECT e.* FROM employees e  
LEFT JOIN departments d ON e.department_id = d.id  
WHERE d.id IS NULL;


q5 

Retrieve employees along with their manager’s name.

SELECT e.name AS Employee, m.name AS Manager  
FROM employees e  
LEFT JOIN employees m ON e.manager_id = m.id;



q6

Find the highest salary in each department.

SELECT department_id, MAX(salary) AS highest_salary  
FROM employees  
GROUP BY department_id;


Get the total number of employees per department.

SELECT department_id, COUNT(*) AS total_employees  
FROM employees  
GROUP BY department_id;



Get the average salary of employees per job title.

SELECT job_title, AVG(salary) AS avg_salary  
FROM employees  
GROUP BY job_title;



q7

Find the second highest salary from the employees table.

SELECT MAX(salary) AS second_highest_salary  
FROM employees  
WHERE salary < (SELECT MAX(salary) FROM employees);

SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;

Offset 1 means skip 1 row 


SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 2;  -- third highest salary 

Offset is used for pagination 

q8

Find employees who earn more than the department average salary.

SELECT * FROM employees e  
WHERE e.salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);
Correlated Subqueries 

q9

Retrieve employees who joined before their manager.

SELECT e.name AS Employee, m.name AS Manager  
FROM employees e  
JOIN employees m ON e.manager_id = m.id  
WHERE e.hire_date < m.hire_date;


