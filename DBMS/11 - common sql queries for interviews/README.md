# SQL Queries for Interviews

##### ORG DB
```sql
CREATE DATABASE ORG;
SHOW DATABASES;
USE ORG;

CREATE TABLE Worker (
    WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    FIRST_NAME CHAR(25),
    LAST_NAME CHAR(25),
    SALARY INT(15),
    JOINING_DATE DATETIME,
    DEPARTMENT CHAR(25)
);

INSERT INTO Worker 
    (WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
    (001, 'Monika', 'Arora', 100000, '14-02-20 09:00:00', 'HR'),
    (002, 'Niharika', 'Verma', 80000, '14-06-11 09:00:00', 'Admin'),
    (003, 'Vishal', 'Singhal', 300000, '14-02-20 09:00:00', 'HR'),
    (004, 'Amitabh', 'Singh', 500000, '14-02-20 09:00:00', 'Admin'),
    (005, 'Vivek', 'Bhati', 500000, '14-06-11 09:00:00', 'Admin'),
    (006, 'Vipul', 'Diwan', 200000, '14-06-11 09:00:00', 'Account'),
    (007, 'Satish', 'Kumar', 75000, '14-01-20 09:00:00', 'Account'),
    (008, 'Geetika', 'Chauhan', 90000, '14-04-11 09:00:00', 'Admin');

CREATE TABLE Bonus (
    WORKER_REF_ID INT,
    BONUS_AMOUNT INT(10),
    BONUS_DATE DATETIME,
    FOREIGN KEY (WORKER_REF_ID) REFERENCES Worker(WORKER_ID) ON DELETE CASCADE
);

INSERT INTO Bonus 
    (WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES
    (001, 5000, '16-02-20'),
    (002, 3000, '16-06-11'),
    (003, 4000, '16-02-20'),
    (001, 4500, '16-02-20'),
    (002, 3500, '16-06-11');

CREATE TABLE Title (
    WORKER_REF_ID INT,
    WORKER_TITLE CHAR(25),
    AFFECTED_FROM DATETIME,
    FOREIGN KEY (WORKER_REF_ID) REFERENCES Worker(WORKER_ID) ON DELETE CASCADE
);

INSERT INTO Title 
    (WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM) VALUES
    (001, 'Manager', '2016-02-20 00:00:00'),
    (002, 'Executive', '2016-06-11 00:00:00'),
    (008, 'Executive', '2016-06-11 00:00:00'),
    (005, 'Manager', '2016-06-11 00:00:00'),
    (004, 'Asst. Manager', '2016-06-11 00:00:00'),
    (007, 'Executive', '2016-06-11 00:00:00'),
    (006, 'Lead', '2016-06-11 00:00:00'),
    (003, 'Lead', '2016-06-11 00:00:00');
```

```sql
SELECT * FROM Worker;
```
| WORKER_ID | FIRST_NAME | LAST_NAME | SALARY | JOINING_DATE        | DEPARTMENT |
|-----------|------------|-----------|--------|---------------------|------------|
| 1         | Monika     | Arora     | 100000 | 2020-02-14 09:00:00 | HR         |
| 2         | Niharika   | Verma     | 80000  | 2020-06-11 09:00:00 | Admin      |
| 3         | Vishal     | Singhal   | 300000 | 2020-02-14 09:00:00 | HR         |
| 4         | Amitabh    | Singh     | 500000 | 2020-02-14 09:00:00 | Admin      |
| 5         | Vivek      | Bhati     | 500000 | 2020-06-11 09:00:00 | Admin      |
| 6         | Vipul      | Diwan     | 200000 | 2020-06-11 09:00:00 | Account    |
| 7         | Satish     | Kumar     | 75000  | 2020-01-20 09:00:00 | Account    |
| 8         | Geetika    | Chauhan   | 90000  | 2020-04-11 09:00:00 | Admin      |

```sql
SELECT * FROM Bonus;
```
| WORKER_REF_ID | BONUS_AMOUNT | BONUS_DATE          |
|---------------|--------------|---------------------|
| 1             | 5000         | 2020-02-16 00:00:00 |
| 2             | 3000         | 2020-06-16 00:00:00 |
| 3             | 4000         | 2020-02-16 00:00:00 |
| 1             | 4500         | 2020-02-16 00:00:00 |
| 2             | 3500         | 2020-06-16 00:00:00 |

```sql
SELECT * FROM Title;
```
| WORKER_REF_ID | WORKER_TITLE | AFFECTED_FROM       |
|---------------|--------------|---------------------|
| 1             | Manager       | 2016-02-20 00:00:00 |
| 2             | Executive     | 2016-06-11 00:00:00 |
| 8             | Executive     | 2016-06-11 00:00:00 |
| 5             | Manager       | 2016-06-11 00:00:00 |
| 4             | Asst. Manager  | 2016-06-11 00:00:00 |
| 7             | Executive     | 2016-06-11 00:00:00 |
| 6             | Lead           | 2016-06-11 00:00:00 |
| 3             | Lead           | 2016-06-11 00:00:00 |

---

##### Q-1. Write an SQL query to fetch “FIRST_NAME” from Worker table using the alias name as <WORKER_NAME>.
```sql
SELECT first_name AS worker_name FROM worker;
```

##### Q-2. Write an SQL query to fetch “FIRST_NAME” from Worker table in upper case.
```sql
SELECT UPPER(first_name) FROM worker;
```

##### Q-3. Write an SQL query to fetch unique values of DEPARTMENT from Worker table.
```sql
SELECT DISTINCT department FROM worker;
```

##### Q-4. Write an SQL query to print the first three characters of  FIRST_NAME from Worker table.
```sql
SELECT SUBSTRING(first_name, 1, 3) FROM worker;
```

##### Q-5. Write an SQL query to find the position of the alphabet (‘b’) in the first name column ‘Amitabh’ from Worker table.
```sql
SELECT INSTR(first_name, 'B') FROM worker WHERE first_name = 'Amitabh';
```

##### Q-6. Write an SQL query to print the FIRST_NAME from Worker table after removing white spaces from the right side.
```sql
SELECT RTRIM(first_name) FROM worker;
```

##### Q-7. Write an SQL query to print the DEPARTMENT from Worker table after removing white spaces from the left side.
```sql
SELECT LTRIM(first_name) FROM worker;
```

##### Q-8. Write an SQL query that fetches the unique values of DEPARTMENT from Worker table and prints its length.
```sql
SELECT DISTINCT department, LENGTH(department) FROM worker;
```

##### Q-9. Write an SQL query to print the FIRST_NAME from Worker table after replacing ‘a’ with ‘A’.
```sql
SELECT REPLACE(first_name, 'a', 'A')  FROM worker;
```

##### Q-10. Write an SQL query to print the FIRST_NAME and LAST_NAME from Worker table into a single column COMPLETE_NAME.
###### A space char should separate them.
```sql
SELECT CONCAT(first_name, ' ', last_name) AS complete_name FROM worker;
```

##### Q-11. Write an SQL query to print all Worker details from the Worker table order by FIRST_NAME Ascending.
```sql
SELECT * FROM worker ORDER BY first_name;
```

##### Q-12. Write an SQL query to print all Worker details from the Worker table order by 
###### FIRST_NAME Ascending and DEPARTMENT Descending.
```sql
SELECT * FROM worker ORDER BY first_name ASC, department DESC;
```

##### Q-13. Write an SQL query to print details for Workers with the first name as “Vipul” and “Satish” from Worker table.
```sql
SELECT * FROM worker WHERE first_name IN ('Vipul', 'Satish');
```

##### Q-14. Write an SQL query to print details of workers excluding first names, “Vipul” and “Satish” from Worker table.
```sql
SELECT * FROM worker WHERE first_name NOT IN ('Vipul', 'Satish');
```

##### Q-15. Write an SQL query to print details of Workers with DEPARTMENT name as “Admin*”.
```sql
SELECT * FROM worker WHERE department LIKE 'Admin%';
```

##### Q-16. Write an SQL query to print details of the Workers whose FIRST_NAME contains ‘a’.
```sql
SELECT * FROM worker WHERE first_name LIKE '%a%';
```

##### Q-17. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘a’.
```sql
SELECT * FROM worker WHERE first_name LIKE '%a';
```

##### Q-18. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘h’ and contains six alphabets.
```sql
SELECT * FROM worker WHERE first_name LIKE '_____h';
```

##### Q-19. Write an SQL query to print details of the Workers whose SALARY lies between 100000 and 500000.
```sql
SELECT * FROM worker WHERE salary BETWEEN 100000 AND 500000;
```

##### Q-20. Write an SQL query to print details of the Workers who have joined in Feb’2014.
```sql
SELECT * FROM worker WHERE YEAR(joining_date) = 2014 AND MONTH(joining_date) = 02;
```

##### Q-21. Write an SQL query to fetch the count of employees working in the department ‘Admin’.
```sql
SELECT department, COUNT(*) FROM worker WHERE department = 'Admin';
```

##### Q-22. Write an SQL query to fetch worker full names with salaries >= 50000 and <= 100000.
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM worker
WHERE salary BETWEEN 50000 AND 100000;
```

##### Q-23. Write an SQL query to fetch the no. of workers for each department in the descending order.
```sql
SELECT department, COUNT(worker_id) AS no_of_workers FROM worker GROUP BY department
ORDER BY no_of_workers DESC;
```

##### Q-24. Write an SQL query to print details of the Workers who are also Managers.
```sql
SELECT w.* FROM worker AS w INNER JOIN title AS t ON w.worker_id = t.worker_ref_id
WHERE t.worker_title = 'Manager';
```

##### Q-25. Write an SQL query to fetch number (more than 1) of same titles in the ORG of different types.
```sql
SELECT worker_title, COUNT(*) AS title_count FROM title GROUP BY worker_title HAVING title_count > 1;
```

##### Q-26. Write an SQL query to show only odd rows from a table.
```sql
SELECT * FROM worker WHERE MOD(WORKER_ID, 2) != 0;
```
```sql
SELECT * FROM worker WHERE MOD(WORKER_ID, 2) <> 0;
```

##### Q-27. Write an SQL query to show only even rows from a table. 
```sql
SELECT * FROM worker WHERE MOD(WORKER_ID, 2) = 0;
```

##### Q-28. Write an SQL query to clone a new table from another table.
```sql
CREATE TABLE worker_clone LIKE worker;
INSERT INTO worker_clone SELECT * FROM worker;
SELECT * FROM worker_clone;
```

##### Q-29. Write an SQL query to fetch intersecting records of two tables.
```sql
SELECT worker.* FROM worker INNER JOIN worker_clone USING(worker_id);
```

##### Q-30. Write an SQL query to show records from one table that another table does not have.
###### MINUS
```sql
SELECT worker.* FROM worker LEFT JOIN worker_clone USING(worker_id)
WHERE worker_clone.worker_id IS NULL;
```

##### Q-31. Write an SQL query to show the current date and time.
###### DUAL
```sql
SELECT CURRENT_DATE AS current_date;
SELECT NOW() AS current_datetime;
```

##### Q-32. Write an SQL query to show the top n (say 5) records of a table order by descending salary.
```sql
SELECT * FROM worker ORDER BY salary DESC LIMIT 5;
```

##### Q-33. Write an SQL query to determine the nth (say n=5) highest salary from a table.
```sql
SELECT * FROM worker ORDER BY salary DESC LIMIT 4, 1;
```

##### Q-34. Write an SQL query to determine the 5th highest salary without using LIMIT keyword.
```sql
SELECT salary FROM worker w1
WHERE 4 = (
  SELECT COUNT(DISTINCT w2.salary)
  FROM worker w2
  WHERE w2.salary >= w1.salary
);
```
 
##### Q-35. Write an SQL query to fetch the list of employees with the same salary.
```sql
SELECT w1.* FROM worker w1, worker w2
WHERE w1.salary = w2.salary AND w1.worker_id != w2.worker_id;
```

##### Q-36. Write an SQL query to show the second highest salary from a table using sub-query.
```sql
SELECT MAX(salary) FROM worker WHERE salary NOT IN (SELECT MAX(salary) FROM worker);
```

##### Q-37. Write an SQL query to show one row twice in results from a table.
```sql
SELECT * FROM worker
UNION ALL
SELECT * FROM worker ORDER BY worker_id;
```

##### Q-38. Write an SQL query to list worker_id who does not get bonus.
```sql
SELECT worker_id FROM worker WHERE worker_id NOT IN (SELECT worker_ref_id FROM bonus);
```

##### Q-39. Write an SQL query to fetch the first 50% records from a table.
```sql
SELECT * FROM worker WHERE worker_id <= (SELECT COUNT(worker_id) / 2 FROM worker);
```

##### Q-40. Write an SQL query to fetch the departments that have less than 4 people in it.
```sql
SELECT department, COUNT(department) AS dep_count FROM worker
GROUP BY department HAVING dep_count < 4;
```

##### Q-41. Write an SQL query to show all departments along with the number of people in there.
```sql
SELECT department, COUNT(department) AS dep_count FROM worker GROUP BY department;
```

##### Q-42. Write an SQL query to show the last record from a table.
```sql
SELECT * FROM worker WHERE worker_id = (SELECT MAX(worker_id) FROM worker);
```

##### Q-43. Write an SQL query to fetch the first row of a table.
```sql
SELECT * FROM worker WHERE worker_id = (SELECT MIN(worker_id) FROM worker);
```

##### Q-44. Write an SQL query to fetch the last five records from a table.
```sql
(SELECT * FROM worker ORDER BY worker_id DESC LIMIT 5) ORDER BY worker_id;
```

##### Q-45. Write an SQL query to print the name of employees having the highest salary in each department.
```sql
SELECT w.department, w.first_name, w.salary FROM
  (SELECT MAX(salary) AS max_salary, department FROM worker GROUP BY department) temp
  INNER JOIN worker w ON temp.department = w.department AND temp.max_salary = w.salary;
```

##### Q-46. Write an SQL query to fetch three max salaries from a table using co-related subquery
```sql
SELECT DISTINCT salary FROM worker w1
WHERE 3 >= (SELECT COUNT(DISTINCT salary) FROM worker w2 WHERE w1.salary <= w2.salary)
ORDER BY w1.salary DESC;
```
###### DRY RUN AFTER REVISING THE CORELATED SUBQUERY CONCEPT FROM LEC-9.
```sql
SELECT DISTINCT salary FROM worker ORDER BY salary DESC LIMIT 3;
```

##### Q-47. Write an SQL query to fetch three min salaries from a table using co-related subquery
```sql
SELECT DISTINCT salary FROM worker w1
WHERE 3 >= (SELECT COUNT(DISTINCT salary) FROM worker w2 WHERE w1.salary >= w2.salary)
ORDER BY w1.salary DESC;
```
##### Q-48. Write an SQL query to fetch nth max salaries from a table.
```sql
SELECT DISTINCT salary FROM worker w1
WHERE n >= (SELECT COUNT(DISTINCT salary) FROM worker w2 WHERE w1.salary <= w2.salary)
ORDER BY w1.salary DESC;
```

##### Q-49. Write an SQL query to fetch departments along with the total salaries paid for each of them.
```sql
SELECT department, SUM(salary) AS dep_salary FROM worker GROUP BY department
ORDER BY dep_salary DESC;
```

##### Q-50. Write an SQL query to fetch the names of workers who earn the highest salary.
```sql
SELECT first_name, salary FROM worker WHERE salary = (SELECT MAX(salary) FROM worker);
```
