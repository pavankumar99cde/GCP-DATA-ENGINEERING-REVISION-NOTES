**101. List the employee names and his average salary department wise.**
```sql
-- Method 1: Using Group By clause
SELECT d.DNAME,e.ENAME , AVG(e.SAL) as AverageSalary
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
GROUP BY d.DNAME, e.ENAME;
-- Method 2 : using subquery
SELECT d.DNAME,e.ENAME, (SELECT AVG(SAL) FROM EMPY e2 WHERE e2.DEPTNO = e.DEPTNO) AS AverageSalary
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO;
```

**102. Find out least 5 earners of the company.**

```sql
-- Method 1: Using ORDER BY and LIMIT
SELECT * FROM EMPY
ORDER BY SAL ASC
LIMIT 5;

-- Method 2: Using Row Number (more portable if limit is not available)
-- (Syntax for row_number might vary depending on specific database)
SELECT * FROM (
  SELECT *, ROW_NUMBER() OVER (ORDER BY SAL ASC) as rn
  FROM EMPY
) as subquery WHERE rn <= 5;

```

**103. Find out emps whose salaries greater than salaries of their managers.**

```sql
-- Method 1: Using Self-Join
SELECT e1.* FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e1.SAL > e2.SAL;

-- Method 2: Using a Subquery
SELECT e1.* FROM EMPY e1
WHERE e1.SAL > (SELECT SAL FROM EMPY e2 WHERE e2.EMPNO = e1.MGR)
```

**104. List the managers who are not working under the president.**

```sql
-- Method 1: Using NOT IN
SELECT * FROM EMPY
WHERE JOB = 'MANAGER'
AND MGR NOT IN (SELECT EMPNO FROM EMPY WHERE JOB = 'PRESIDENT');

-- Method 2: Using LEFT JOIN
SELECT m.* FROM EMPY m
LEFT JOIN EMPY p ON m.MGR = p.EMPNO AND p.JOB = 'PRESIDENT'
WHERE m.JOB = 'MANAGER' AND p.EMPNO IS NULL;

```

**105. List the records from emp whose deptno is not in dept.**

```sql
-- Method 1: Using NOT IN
SELECT * FROM EMPY
WHERE DEPTNO NOT IN (SELECT DEPTNO FROM DEPT);

-- Method 2: Using LEFT JOIN and IS NULL
SELECT e.* FROM EMPY e
LEFT JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE d.DEPTNO IS NULL;
```

**106. List the Name, Salary, Comm and Net Pay is more than any other employee.**

```sql
-- Method 1: Using subquery and ALL clause
SELECT ENAME, SAL, COMM FROM EMPY
WHERE (SAL + IFNULL(COMM, 0)) >= ALL (SELECT (SAL + IFNULL(COMM, 0)) FROM EMPY);

-- Method 2: Using ORDER BY and LIMIT
SELECT ENAME, SAL, COMM FROM EMPY
ORDER BY (SAL + IFNULL(COMM, 0)) DESC LIMIT 1;
```

**107. List the Enames who are retiring after 31-Dec-89 the max Job period is 20Y.**

```sql
-- Method 1: using date logic in where clause
SELECT ENAME FROM EMPY
WHERE DATE_ADD(HIREDATE, INTERVAL 20 YEAR) > '1989-12-31';
-- Method 2 : date comparison
SELECT ENAME FROM EMPY
WHERE YEAR(DATE_ADD(HIREDATE, INTERVAL 20 YEAR)) > 1989;
```

**108. List those Emps whose Salary is odd value.**

```sql
-- Method 1: Using the Modulo operator (%)
SELECT * FROM EMPY
WHERE SAL % 2 <> 0;

-- Method 2:  Using bitwise AND (less common)
SELECT * FROM EMPY
WHERE SAL & 1 = 1;
```

**109. List the emp’s whose Salary contain 3 digits.**

```sql
-- Method 1: Using LIKE and length
SELECT * FROM EMPY
WHERE CAST(SAL as CHAR) LIKE '___' ;
-- Method 2: Using BETWEEN (Specific for this case, general length check needs method 1)
SELECT * FROM EMPY WHERE SAL BETWEEN 100 AND 999;
```

**110. List the emps who joined in the month of DEC.**

```sql
-- Method 1: Using MONTH function
SELECT * FROM EMPY
WHERE MONTH(HIREDATE) = 12;

-- Method 2: Using date ranges for December
SELECT * FROM EMPY WHERE HIREDATE BETWEEN '1900-12-01' AND '2100-12-31';
```

**111. List the emps whose names contains ‘A’.**

```sql
-- Method 1: Using LIKE
SELECT * FROM EMPY
WHERE ENAME LIKE '%A%';

-- Method 2: Using case insensitivity (depending on the DB)
SELECT * FROM EMPY WHERE UPPER(ENAME) LIKE '%A%';
```

**112. List the emps whose Deptno is available in his Salary.**
```sql
-- Method 1: Using LIKE and CAST
SELECT * FROM EMPY
WHERE CAST(SAL AS CHAR) LIKE CONCAT('%',CAST(DEPTNO AS CHAR),'%');

-- Method 2 : Using find_in_set 
-- (only useful for some databases)
SELECT * FROM EMPY
WHERE FIND_IN_SET(DEPTNO,SAL);

```

**113. List the emps whose first 2 chars from Hiredate=last 2 characters of Salary.**
```sql
-- Method 1: Using SUBSTR, CAST, and comparison
SELECT *
FROM EMPY
WHERE SUBSTR(CAST(HIREDATE AS CHAR), 3, 2) = SUBSTR(CAST(SAL AS CHAR),LENGTH(CAST(SAL AS CHAR))-1, 2);
-- Method 2 : using string manupulation
SELECT *
FROM EMPY
WHERE RIGHT(CAST(SAL AS CHAR),2) = SUBSTR(CAST(HIREDATE as CHAR), 3,2);
```

**114. List the emps Whose 10% of Salary is equal to year of joining.**
```sql
-- Method 1: using calculations and cast
SELECT * FROM EMPY
WHERE CAST(SAL*0.1 AS INT) = YEAR(HIREDATE);

-- Method 2: (Same logic different operators)
SELECT * FROM EMPY WHERE FLOOR(SAL * 0.1) = YEAR(HIREDATE);
```

**115. List first 50% of chars of Ename in Lower Case and remaining are upper C**

```sql
-- Method 1: Using SUBSTR, LOWER, UPPER, and LENGTH
SELECT
  CONCAT(
    LOWER(SUBSTR(ENAME, 1, FLOOR(LENGTH(ENAME) / 2))),
    UPPER(SUBSTR(ENAME, FLOOR(LENGTH(ENAME) / 2) + 1))
  ) AS modified_ename
FROM EMPY;

-- Method 2: (Similar logic, different DB functions)
SELECT
  CONCAT(
    LCASE(SUBSTR(ENAME, 1, LENGTH(ENAME)/2 )),
    UCASE(SUBSTR(ENAME, LENGTH(ENAME)/2 + 1))
  ) AS modified_ename
FROM EMPY;
```

**116. List the Dname whose No. of Emps is =to number of chars in the Dname.**

```sql
-- Method 1: Using JOIN, GROUP BY, HAVING, and LENGTH
SELECT d.DNAME
FROM DEPT d
JOIN EMPY e ON d.DEPTNO = e.DEPTNO
GROUP BY d.DNAME
HAVING LENGTH(d.DNAME) = COUNT(*);

-- Method 2: Using Subquery and Length
SELECT DNAME FROM DEPT
WHERE LENGTH(DNAME) = (SELECT COUNT(*) FROM EMPY WHERE DEPTNO=DEPT.DEPTNO GROUP BY DEPTNO);
```

**117. List the emps those who joined in company before 15th of the month.**

```sql
-- Method 1: Using DAY() function
SELECT *
FROM EMPY
WHERE DAY(HIREDATE) < 15;

-- Method 2: Using Date comparison
SELECT * FROM EMPY WHERE HIREDATE < DATE_ADD(HIREDATE, INTERVAL (15-DAY(HIREDATE)) DAY);
```

**118. List the Dname, no of chars of which is = no. of emp’s in any other Dept.**

```sql
-- Method 1: Using subquery and a join
SELECT d1.DNAME
FROM DEPT d1
WHERE LENGTH(d1.DNAME) IN (SELECT COUNT(*) FROM EMPY e WHERE e.DEPTNO != d1.DEPTNO GROUP BY e.DEPTNO);

-- Method 2: Using self join
SELECT d1.DNAME FROM DEPT d1
JOIN (SELECT DEPTNO, COUNT(*) AS emp_count FROM EMPY GROUP BY DEPTNO) as emp_counts
ON LENGTH(d1.DNAME) = emp_counts.emp_count
WHERE d1.DEPTNO != emp_counts.DEPTNO;

```

**119. List the emps who are working as Managers.**

```sql
-- Method 1:  Using WHERE clause
SELECT *
FROM EMPY
WHERE JOB = 'MANAGER';
-- Method 2: Using subquery
SELECT * FROM EMPY WHERE EMPNO IN (SELECT EMPNO FROM EMPY WHERE JOB='MANAGER');

```

**120. List THE Name of dept where highest no.of emps are working.**

```sql
-- Method 1: Using ORDER BY, LIMIT and JOIN
SELECT d.DNAME
FROM DEPT d
JOIN EMPY e ON d.DEPTNO = e.DEPTNO
GROUP BY d.DEPTNO
ORDER BY COUNT(*) DESC
LIMIT 1;

-- Method 2: Using subquery and max count
SELECT DNAME FROM DEPT
WHERE DEPTNO = (SELECT DEPTNO FROM EMPY GROUP BY DEPTNO ORDER BY COUNT(*) DESC LIMIT 1);
```

**121. Count the No.of emps who are working as ‘Managers’(using set option).**
*(The "set option" wording here is a bit ambiguous, and might refer to a specific DB feature or a variable setting.
I will interpret this as meaning to provide the count using a subquery or a CTE)*
```sql
-- Method 1: Using subquery and count
SELECT COUNT(*) FROM (SELECT * FROM EMPY WHERE JOB='MANAGER') as subquery;

-- Method 2: Simple count with where clause
SELECT COUNT(*) FROM EMPY WHERE JOB='MANAGER';
```

**122. List the emps who joined in the company on the same date.**

```sql
-- Method 1: Using Self Join
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.HIREDATE = e2.HIREDATE
WHERE e1.EMPNO <> e2.EMPNO;
-- Method 2: using subquery
SELECT * from EMPY WHERE HIREDATE IN(SELECT HIREDATE FROM EMPY GROUP BY HIREDATE HAVING COUNT(*) > 1)
```

**123. List the details of the emps whose Grade is equal to one tenth of Sales Dept.**

```sql
-- Method 1: Using subqueries
SELECT * FROM EMPY
WHERE GRADE = (SELECT FLOOR(AVG(SAL)/10) FROM EMPY WHERE DEPTNO=(SELECT DEPTNO FROM DEPT WHERE DNAME='SALES'));

-- Method 2: Using join
SELECT e.* FROM EMPY e
JOIN (SELECT FLOOR(AVG(SAL)/10) as avgsal FROM EMPY
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME='SALES')) AS subquery
ON e.GRADE = subquery.avgsal;
```

**124. List the name of the dept where more than average no. of emps are working.**

```sql
-- Method 1: Using HAVING clause
SELECT d.DNAME
FROM DEPT d
JOIN EMPY e ON d.DEPTNO = e.DEPTNO
GROUP BY d.DNAME
HAVING COUNT(*) > (SELECT AVG(emp_count) FROM (SELECT COUNT(*) as emp_count FROM EMPY GROUP BY DEPTNO) as emp_counts);

-- Method 2: Using Subquery
SELECT d.DNAME
FROM DEPT d
WHERE d.DEPTNO IN (
    SELECT DEPTNO
    FROM EMPY
    GROUP BY DEPTNO
    HAVING COUNT(*) > (
        SELECT AVG(emp_count)
        FROM (SELECT COUNT(*) as emp_count FROM EMPY GROUP BY DEPTNO) as subquery
    )
);
```

**125. List the Managers name who is having max no.of emps working under him.**

```sql
-- Method 1: Using order by and limit
SELECT e2.ENAME
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR=e2.EMPNO
WHERE e2.JOB = 'MANAGER'
GROUP BY e1.MGR
ORDER BY COUNT(*) DESC LIMIT 1;

-- Method 2: using subquery
SELECT ENAME FROM EMPY
WHERE EMPNO = (SELECT MGR
FROM EMPY
GROUP BY MGR
ORDER BY COUNT(*) DESC LIMIT 1);
```

**126. List the Ename and Sal is increased by -- 15% and expressed as no.of Dollars.**

```sql
-- Method 1:  Using basic calculation
SELECT ENAME, CAST((SAL * 1.15) AS DECIMAL(10, 0)) AS increased_salary_dollars
FROM EMPY;

-- Method 2: same logic in subquery
SELECT ENAME, (CAST((SAL * 1.15) AS DECIMAL(10, 0))) AS increased_salary_dollars
FROM (SELECT ENAME, SAL FROM EMPY) AS subquery;
```

**127. Produce the output of EMP table ‘EMP_AND_JOB’ for Ename and Job.**
*(This looks like a formatting question. I'll answer as if outputting a combined field)*

```sql
-- Method 1: Using CONCAT
SELECT CONCAT(ENAME, ' (', JOB, ')') AS EMP_AND_JOB
FROM EMPY;

-- Method 2: Using string concatenation operators (depends on database)
SELECT ENAME || ' (' || JOB || ')' as EMP_AND_JOB FROM EMPY;
```

**128. Produce the following output from EMP. EMPLOYEE SMITH (clerk) ALLEN (Salesman)**
*(Similar to the formatting question above, but adds the literal "EMPLOYEE")*

```sql
-- Method 1: Using CONCAT
SELECT CONCAT('EMPLOYEE ', ENAME, ' (', JOB, ')')
FROM EMPY;

-- Method 2: using string concatenation (db dependent)
SELECT 'EMPLOYEE ' || ENAME || ' (' || JOB || ')' as output
FROM EMPY;
```

**130) List the emps with Hire date in format June 4, 1988.**

```sql
-- Method 1: using DATE_FORMAT
SELECT ENAME, DATE_FORMAT(HIREDATE, '%M %e, %Y') as formatted_hire_date
FROM EMPY;

-- Method 2: Database-specific date formatting (like strftime in SQLite)
SELECT ENAME, strftime('%B %d, %Y', HIREDATE) AS formatted_hire_date
FROM EMPY;
```

**131)Print a list of emp’s Listing ‘just salary’ if Salary is more than 1500, on target if Salary is -- 1500 and ‘Below -- 1500’ if Salary is less than-- 1500.**

```sql
-- Method 1: Using CASE statement
SELECT ENAME,
       CASE
         WHEN SAL > 1500 THEN 'just salary'
         WHEN SAL = 1500 THEN 'on target'
         ELSE 'Below 1500'
       END AS salary_status
FROM EMPY;

-- Method 2: Using IF statement (alternative)
SELECT ENAME,
       IF(SAL > 1500, 'just salary', IF(SAL = 1500, 'on target', 'Below 1500')) AS salary_status
FROM EMPY;
```
**132)Write a query which returns the day of the week for any date entered in format ‘DD-MM-YY’.**
*(This will require date formatting as well as functions to return the day of the week - database-specific)*
```sql
-- Method 1: Using DATE_FORMAT (MySQL)
SELECT DATE_FORMAT('2024-01-26', '%W');

-- Method 2: Using strftime (SQLite)
SELECT strftime('%w', '2024-01-26'); -- returns 0-6 for day of week

-- Method 3: Using DAYNAME (SQL Server)
SELECT DATENAME(weekday,'2024-01-26');
```
**Note**: The specific function used depends on your SQL database system. You might use `DAYNAME`, `strftime`, or other similar functions.

**133)Write a query to calculate the length of service of any employee with the company, use DEFINE to avoid repetitive typing of functions.**
*(Here I will show how to do a calculation and include that calculation in the output as a variable)*

```sql
-- Method 1: using calculation in select
SELECT ENAME, (YEAR(CURDATE()) - YEAR(HIREDATE)) as length_of_service
FROM EMPY;

-- Method 2: using a common table expression
WITH EmployeeService AS (
    SELECT ENAME, (YEAR(CURDATE()) - YEAR(HIREDATE)) AS service_years
    FROM EMPY
)
SELECT ENAME, service_years
FROM EmployeeService;
```
**Note**: `DEFINE` is not standard SQL, but some DBs may have specific ways to declare variables. I have used a CTE as a general solution.

**134)Give a string of format ‘NN/NN’, verify that the first and last two characters are numbers and that the middle character is’/’. 
Print the expression ‘YES’ if valid, ‘NO’ if not valid. Use the following values to test your solution. ‘-- 12/34’,’0-- 1/-- 1a’, ‘99/98’.**
```sql
-- Method 1: Using CASE and LIKE
SELECT
    CASE
        WHEN '12/34' LIKE '[0-9][0-9]/[0-9][0-9]' THEN 'YES'
        ELSE 'NO'
    END as result1,
	CASE
        WHEN '01/1a' LIKE '[0-9][0-9]/[0-9][0-9]' THEN 'YES'
        ELSE 'NO'
    END as result2,
	CASE
        WHEN '99/98' LIKE '[0-9][0-9]/[0-9][0-9]' THEN 'YES'
        ELSE 'NO'
    END as result3;

-- Method 2: Using regex functions (db dependent)
-- (MySQL example)
SELECT
    CASE
        WHEN '12/34' REGEXP '^[0-9]{2}/[0-9]{2}$' THEN 'YES'
        ELSE 'NO'
    END as result1,
    CASE
        WHEN '01/1a' REGEXP '^[0-9]{2}/[0-9]{2}$' THEN 'YES'
        ELSE 'NO'
    END as result2,
	CASE
        WHEN '99/98' REGEXP '^[0-9]{2}/[0-9]{2}$' THEN 'YES'
        ELSE 'NO'
    END as result3;

```
**Note**: Regex functionality depends on your database system. LIKE statements use standard wildcards.

**135)Emps hired on or before 15th of any month are paid on the last Friday of that month those hired after 15th are paid on the first
Friday of the following month. Print a list of emps their hire date and the first pay date. Sort on hire date.**
*(This requires date calculations and specific DB functions)*
```sql
-- Method 1: (Database-specific logic - MySQL)
SELECT ENAME, HIREDATE,
       CASE
           WHEN DAY(HIREDATE) <= 15
           THEN LAST_DAY(HIREDATE) - INTERVAL (DAYOFWEEK(LAST_DAY(HIREDATE)) - 6) DAY
           ELSE  LAST_DAY(HIREDATE + INTERVAL 1 MONTH)  - INTERVAL (DAYOFWEEK(LAST_DAY(HIREDATE + INTERVAL 1 MONTH)) - 6) DAY
        END AS pay_date
FROM EMPY
ORDER BY HIREDATE;

-- Method 2: Using Common Table expression
WITH PayDates AS (
SELECT ENAME, HIREDATE, CASE
WHEN DAY(HIREDATE) <= 15
THEN LAST_DAY(HIREDATE) - INTERVAL (DAYOFWEEK(LAST_DAY(HIREDATE)) - 6) DAY
ELSE LAST_DAY(HIREDATE + INTERVAL 1 MONTH) - INTERVAL (DAYOFWEEK(LAST_DAY(HIREDATE + INTERVAL 1 MONTH)) - 6) DAY
END AS pay_date
FROM EMPY)
SELECT ENAME, HIREDATE, pay_date
FROM PayDates
ORDER BY HIREDATE;

```
**Note**: `LAST_DAY` ,`DAYOFWEEK`,`INTERVAL`  functions used above are MySQL Specific, you may need different function for your database.

**136)Count the no. of characters without considering spaces for each name.**

```sql
-- Method 1: Using REPLACE and LENGTH
SELECT ENAME, LENGTH(REPLACE(ENAME, ' ', '')) AS char_count
FROM EMPY;

-- Method 2: using string function and length
SELECT ENAME, LENGTH(TRIM(ENAME)) as char_count
FROM EMPY;

```
**137)Find out the emps who are getting decimal value in their Sal without using like operator.**

```sql
-- Method 1: using string function
SELECT *
FROM EMPY
WHERE CAST(SAL as CHAR) LIKE '%.%'

-- Method2: Using data type & check(Database dependent and not fully guaranteed, might need implicit type casting or regex)
SELECT * FROM EMPY WHERE SAL<>FLOOR(SAL);

```

**Note**:  Some SQL databases may not have implicit typecasting and may need functions like `REGEXP` or casting to `VARCHAR` and checking 
`LIKE '% .%'` which uses a `LIKE` operator.

**138)List those emps whose Salary contains first four digit of their Deptno**

```sql
-- Method 1: Using LIKE and SUBSTR with CAST
SELECT *
FROM EMPY
WHERE CAST(SAL AS CHAR) LIKE CONCAT(SUBSTR(CAST(DEPTNO as CHAR),1,4),'%');
-- Method 2: using string function
SELECT *
FROM EMPY
WHERE SUBSTR(CAST(SAL as CHAR),1,4) = SUBSTR(CAST(DEPTNO as CHAR),1,4);
```

**139)List those Managers who are getting less than his emps Salary.**
```sql
-- Method 1: Using self join and AVG
SELECT e1.*
FROM EMPY e1
JOIN (SELECT MGR, AVG(SAL) AS avg_sal FROM EMPY GROUP BY MGR) AS subquery
ON e1.EMPNO = subquery.MGR
WHERE e1.JOB = 'MANAGER' AND e1.SAL < subquery.avg_sal;

-- Method 2: Using self join
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e1.JOB = 'MANAGER'
AND e1.SAL < e2.SAL;

```

**140)Print the details of all the emps who are sub-ordinates to Blake.**

```sql
-- Method 1: Using subquery
SELECT *
FROM EMPY
WHERE MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'BLAKE');

-- Method 2: Using join clause
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e2.ENAME = 'BLAKE';
```
**141)List the emps who are working as Managers using co-related sub- query.**

```sql
-- Method 1: Correlated subquery (Using EXISTS)
SELECT *
FROM EMPY e1
WHERE EXISTS (SELECT 1 FROM EMPY e2 WHERE e2.EMPNO = e1.EMPNO AND e2.JOB = 'MANAGER');

-- Method 2:  Using a simple subquery (less efficient)
SELECT * FROM EMPY WHERE EMPNO IN(SELECT EMPNO FROM EMPY WHERE JOB='MANAGER');
```
**142)List the emps whose Mgr name is ‘Jones’ and also with his Manager name.**

```sql
-- Method 1: Using Self-Join
SELECT e1.ENAME AS employee_name, e2.ENAME AS manager_name
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e2.ENAME = 'JONES';

-- Method 2: using subquery
SELECT e.ENAME AS employee_name, (SELECT ENAME FROM EMPY WHERE EMPNO=e.MGR) as manager_name
FROM EMPY e WHERE e.MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'JONES');
```

**143)Define a variable representing the expression used to calculate on emps total annual remuneration use the variable in a statement, 
    which finds all emps who can earn 30000 a year or more.**

```sql
-- Method 1: using CTE
WITH AnnualRemuneration AS (
    SELECT EMPNO, ENAME, (SAL + IFNULL(COMM, 0)) * 12 AS annual_remuneration
    FROM EMPY
)
SELECT EMPNO, ENAME
FROM AnnualRemuneration
WHERE annual_remuneration >= 30000;

-- Method 2: using inline subquery
SELECT EMPNO,ENAME FROM EMPY WHERE (SAL+IFNULL(COMM,0))*12 >=30000;
```

**144)Find out how many Managers are their in the company.**

```sql
-- Method 1: Using COUNT and WHERE
SELECT COUNT(*) AS number_of_managers
FROM EMPY
WHERE JOB = 'MANAGER';

-- Method 2: Using subquery
SELECT COUNT(*) FROM (SELECT * FROM EMPY WHERE JOB = 'MANAGER') AS subquery;
```

**145)Find Average salary and Average total remuneration for each Jobtype. Remember Salesman earn commission.**

```sql
-- Method 1:  Using GROUP BY and AVG, with CASE for commission
SELECT JOB,
       AVG(SAL) AS average_salary,
       AVG(SAL + CASE WHEN JOB = 'SALESMAN' THEN IFNULL(COMM, 0) ELSE 0 END) AS average_total_remuneration
FROM EMPY
GROUP BY JOB;

-- Method 2: using subquery (same logic)
SELECT JOB, AVG(SAL), AVG(remuneration) FROM
(SELECT JOB, SAL, (SAL + CASE WHEN JOB='SALESMAN' THEN IFNULL(COMM,0) ELSE 0 END ) AS remuneration
FROM EMPY) AS subquery
GROUP BY JOB;
```

**146)Check whether all the emps numbers are indeed unique.**

```sql
-- Method 1: Using COUNT with DISTINCT and without
SELECT COUNT(*) AS total_emps, COUNT(DISTINCT EMPNO) as unique_empnos
FROM EMPY;

-- Method 2: using having clause
SELECT 'Unique' FROM EMPY
GROUP BY EMPNO
HAVING COUNT(*) = 1;

-- to check if not unique:
SELECT EMPNO from EMPY GROUP BY EMPNO HAVING COUNT(*) > 1;
```
**Note**: If both counts are the same, the employee numbers are unique.

**147)List the emps who are drawing less than -- 1000 Sort the output by Salary.**

```sql
-- Method 1:  Using basic WHERE and ORDER BY
SELECT *
FROM EMPY
WHERE SAL < 1000
ORDER BY SAL;

-- Method 2: Using a subquery (same logic)
SELECT *
FROM (SELECT * FROM EMPY) AS subquery
WHERE SAL < 1000
ORDER BY SAL;
```
**148)List the employee Name, Job, Annual Salary, deptno, Dept name and grade who earn 36000 a year or who are not CLERKS.**

```sql
-- Method 1: Using JOIN and WHERE with OR
SELECT e.ENAME, e.JOB, e.SAL * 12 AS annual_salary, e.DEPTNO, d.DNAME, e.GRADE
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE (e.SAL * 12 >= 36000) OR (e.JOB <> 'CLERK');

-- Method 2: using subqueries
SELECT e.ENAME, e.JOB, e.SAL * 12 AS annual_salary, e.DEPTNO,
(SELECT DNAME from DEPT WHERE DEPTNO = e.DEPTNO), e.GRADE
FROM EMPY e
WHERE (e.SAL * 12 >= 36000) OR (e.JOB <> 'CLERK');
```

**149)Find out the Job that was filled in the first half of 1983 and same job that was filled during the same period of 1984.**

```sql
-- Method 1: Using subquery with IN
SELECT DISTINCT    JOB FROM EMPY WHERE YEAR(HIREDATE) = 1983 AND MONTH(HIREDATE) <=6
AND JOB IN (SELECT JOB FROM EMPY WHERE YEAR(HIREDATE) = 1984 AND MONTH(HIREDATE) <=6);
-- Method 2: self join
SELECT DISTINCT e1.JOB
FROM EMPY e1
JOIN EMPY e2 ON e1.JOB = e2.JOB
WHERE YEAR(e1.HIREDATE) = 1983
  AND MONTH(e1.HIREDATE) <= 6
  AND YEAR(e2.HIREDATE) = 1984
  AND MONTH(e2.HIREDATE) <= 6;
```

**150)Find out the emps who joined in the company before their Managers.**

```sql
-- Method 1: Using self join and date comparison
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR=e2.EMPNO
WHERE e1.HIREDATE < e2.HIREDATE;

-- Method 2: using subquery
SELECT * FROM EMPY
WHERE HIREDATE < (SELECT HIREDATE FROM EMPY WHERE EMPNO=MGR);

```
