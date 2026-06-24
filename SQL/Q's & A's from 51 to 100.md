
**51. List the Emps who are senior to their own MGRS.**

```sql
-- Method 1: Using a Self-Join
SELECT DISTINCT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e1.HIREDATE < e2.HIREDATE;

-- Method 2:  Not practical here (no alternate simple method other than a self join), it's best to use method 1 here as it is very efficient
SELECT DISTINCT  e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e1.HIREDATE < e2.HIREDATE;
```

**52. List the Emps of Deptno 20 whose Jobs are same as Deptno 10.**

```sql
-- Method 1: Using a Subquery with IN
SELECT *
FROM EMPY
WHERE DEPTNO = 20
AND JOB IN (SELECT DISTINCT JOB FROM EMPY WHERE DEPTNO = 10);

-- Method 2: Using a JOIN
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.JOB = e2.JOB
WHERE e1.DEPTNO = 20 AND e2.DEPTNO=10;
```

**53. List the Emps whose Sal is same as FORD or SMITH in desc order of Sal.**

```sql
-- Method 1: Using a Subquery and IN
SELECT *
FROM EMPY
WHERE SAL IN (SELECT SAL FROM EMPY WHERE ENAME IN ('FORD', 'SMITH'))
ORDER BY SAL DESC;

-- Method 2: Using OR in WHERE
SELECT * FROM EMPY 
WHERE SAL = (SELECT SAL FROM EMPY WHERE ENAME = 'FORD')
OR SAL = (SELECT SAL FROM EMPY WHERE ENAME = 'SMITH')
ORDER BY SAL DESC;
```

**54. List the emps Whose Jobs are same as MILLER or Sal is more than ALLEN.**

```sql
-- Method 1: Using Subqueries and OR
SELECT DISTINCT *
FROM EMPY
WHERE JOB = (SELECT JOB FROM EMPY WHERE ENAME = 'MILLER')
   OR SAL > (SELECT DISTINCT SAL FROM EMPY WHERE ENAME = 'ALLEN');

-- Method 2: Using JOIN (can be a bit less readable but shows an alternative approach)
SELECT DISTINCT e1.*
FROM EMPY e1
LEFT JOIN EMPY e2 ON e2.ENAME = 'MILLER' AND e1.JOB = e2.JOB
LEFT JOIN EMPY e3 ON e3.ENAME = 'ALLEN' AND e1.SAL > e3.SAL
WHERE e2.ENAME IS NOT NULL OR e3.ENAME IS NOT NULL;
```

**55. List the Emps whose Sal is > the total remuneration of the SALESMAN.**

```sql
-- Method 1: Using a Subquery with SUM
SELECT *
FROM EMPY
WHERE SAL > (SELECT SUM(SAL + IFNULL(COMM, 0)) FROM EMPY WHERE JOB = 'SALESMAN');

-- Method 2: Using a Derived Table (alternative way of doing the same)
SELECT e.*
FROM EMPY e
JOIN (SELECT SUM(SAL + IFNULL(COMM,0)) AS total_salesman_remuneration FROM EMPY WHERE JOB = 'SALESMAN') AS s
ON e.SAL > s.total_salesman_remuneration;
```

**56. List the emps who are senior to BLAKE working at CHICAGO&BOSTON.**

```sql
-- Method 1: Using a Subquery and JOIN
SELECT DISTINCT  e.*  FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE d.LOC IN ('CHICAGO','BOSTON')
AND e.HIREDATE < (SELECT HIREDATE FROM EMPY WHERE ENAME = 'BLAKE');


-- Method 2: Using multiple conditions (same logic different way)

SELECT DISTINCT  e.* FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE (d.LOC = 'CHICAGO' OR d.LOC = 'BOSTON')
AND e.HIREDATE < (SELECT HIREDATE FROM EMPY WHERE ENAME = 'BLAKE');

```

**57. List the Emps of Grade 3,4 belongs to the dept ACCOUNTING and RESEARCH whose Sal is more than ALLEN and exp more than SMITH in the asc order of EXP.**

```sql
-- Method 1: Using Subqueries and JOINS
SELECT e.*, YEAR(CURDATE()) - YEAR(e.HIREDATE) as EXP
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.GRADE IN (3, 4)
AND d.DNAME IN ('ACCOUNTING', 'RESEARCH')
AND e.SAL > (SELECT DISTINCT SAL FROM EMPY WHERE ENAME = 'ALLEN')
AND (YEAR(CURDATE()) - YEAR(e.HIREDATE)) > (SELECT YEAR(CURDATE()) - YEAR(HIREDATE) FROM EMPY WHERE ENAME = 'SMITH')
ORDER BY EXP ASC;

-- Method 2: Using OR (same logic with OR instead of IN)
SELECT e.*, YEAR(CURDATE()) - YEAR(e.HIREDATE) as EXP
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE (e.GRADE = 3 OR e.GRADE = 4)
AND (d.DNAME = 'ACCOUNTING' OR d.DNAME = 'RESEARCH')
AND e.SAL > (SELECT DISTINCT SAL FROM EMPY WHERE ENAME = 'ALLEN')
AND (YEAR(CURDATE()) - YEAR(e.HIREDATE)) > (SELECT YEAR(CURDATE()) - YEAR(HIREDATE) FROM EMPY WHERE ENAME = 'SMITH')
ORDER BY EXP ASC;
```

**58. List the emps whose jobs same as SMITH or ALLEN.**

```sql
-- Method 1: Using Subquery and IN
SELECT DISTINCT * FROM EMPY
WHERE JOB IN (SELECT JOB FROM EMPY WHERE ENAME IN ('SMITH', 'ALLEN'));

-- Method 2: Using OR clause
SELECT DISTINCT  * FROM EMPY
WHERE JOB = (SELECT JOB FROM EMPY WHERE ENAME = 'SMITH')
OR JOB = (SELECT DISTINCT JOB FROM EMPY WHERE ENAME = 'ALLEN');
```

**59. Write a Query to display the details of emps whose Sal is same as of Any jobs of deptno 10 those that are not found in deptno 20.**
```sql
-- Method 1: Using Subquery with IN and NOT IN
SELECT *
FROM EMPY
WHERE SAL IN (SELECT SAL
            FROM EMPY
            WHERE DEPTNO = 10
            AND JOB NOT IN (SELECT JOB FROM EMPY WHERE DEPTNO=20));


-- Method 2: Using LEFT JOIN AND IS NULL
SELECT e.*
FROM EMPY e
JOIN (SELECT DISTINCT SAL, JOB FROM EMPY WHERE DEPTNO=10) AS s
ON e.SAL = s.SAL
LEFT JOIN EMPY e2 ON e2.JOB = s.JOB AND e2.DEPTNO = 20
WHERE e2.EMPNO IS NULL;
```

**60. List of emps of emp1 who are not found in emp2.**
*(This query is ambiguous as we only have one table EMPY. I will assume you meant to compare EMPY against itself based on EMPNO to see which EMPNO exists in one 'copy' but not the other. Here, I'm using a simple example by filtering EMPNO greater than 7700 as the second set of records)*
```sql
-- Method 1: Using NOT IN
SELECT DISTINCT * FROM EMPY
WHERE EMPNO NOT IN (SELECT EMPNO FROM EMPY WHERE EMPNO > 7700);

-- Method 2: Using LEFT JOIN and IS NULL
SELECT DISTINCT  e1.* FROM EMPY e1
LEFT JOIN EMPY e2 ON e1.EMPNO = e2.EMPNO AND e2.EMPNO > 7700
WHERE e2.EMPNO IS NULL;
```

**61. Find the highest sal of EMP table.**

```sql
-- Method 1: Using MAX aggregate function
SELECT MAX(SAL) AS highest_salary FROM EMPY;

-- Method 2: Using ORDER BY and LIMIT (less performant than max)
SELECT SAL AS highest_salary FROM EMPY ORDER BY SAL DESC LIMIT 1;
```

**62. Find details of highest paid employee.**
```sql
-- Method 1: Using Subquery
SELECT *
FROM EMPY
WHERE SAL = (SELECT MAX(SAL) FROM EMPY);

-- Method 2: Using ORDER BY and LIMIT (less performant than max but more straightforward)
SELECT * FROM EMPY ORDER BY SAL DESC LIMIT 1;
```

**63. Find the highest paid employee of sales department.**

```sql
-- Method 1: Using Subquery with MAX
SELECT *
FROM EMPY
WHERE SAL = (SELECT MAX(SAL) FROM EMPY WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES'))
AND DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES');

-- Method 2: Using ORDER BY and LIMIT with subquery
SELECT * FROM EMPY
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES')
ORDER BY SAL DESC LIMIT 1;
```

**64. List the most recently hired emp of grade3 belongs to location CHICAGO.**

```sql
-- Method 1: Using Subquery and MAX
SELECT e.*
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.HIREDATE = (SELECT MAX(HIREDATE)
                    FROM EMPY
                    JOIN DEPT ON EMPY.DEPTNO = DEPT.DEPTNO
                    WHERE GRADE = 3
                    AND LOC = 'CHICAGO')
AND e.GRADE = 3
AND d.LOC = 'CHICAGO';
-- Method 2 : Using Order by and limit
SELECT e.*
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.GRADE = 3
AND d.LOC = 'CHICAGO'
ORDER BY e.HIREDATE DESC LIMIT 1;

```

**65. List the employees who are senior to most recently hired employee working under king.**

```sql
-- Method 1: Using nested subquery
SELECT DISTINCT  * FROM EMPY
WHERE HIREDATE < (SELECT MAX(HIREDATE)
                FROM EMPY
                WHERE MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'KING'));

-- Method 2: Using JOIN and subquery (more readable alternative to subquery)
SELECT DISTINCT  e.* FROM EMPY e
JOIN (SELECT MAX(HIREDATE) AS max_hire_date
      FROM EMPY
      WHERE MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'KING')) AS subquery
ON e.HIREDATE < subquery.max_hire_date;
```

**66. List the details of the employee belongs to newyork with grade 3to5 except ‘PRESIDENT’ whose sal> the highest paid employee of Chicago in a group where there is manager and salesman not working under king**

```sql
-- Method 1: Using Subqueries and Joins
SELECT DISTINCT e.*
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE d.LOC = 'NEWYORK'
AND e.GRADE BETWEEN 3 AND 5
AND e.JOB <> 'PRESIDENT'
AND e.SAL > (SELECT MAX(SAL) FROM EMPY  JOIN DEPT ON EMPY.DEPTNO = DEPT.DEPTNO WHERE LOC = 'CHICAGO')
AND EXISTS (SELECT * FROM EMPY WHERE JOB IN ('MANAGER', 'SALESMAN') AND MGR IS NOT NULL AND  MGR <> (SELECT EMPNO FROM EMPY WHERE ENAME='KING'));

-- Method 2: Using separate subqueries for clarity
SELECT DISTINCT e.*
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE d.LOC = 'NEWYORK'
AND e.GRADE BETWEEN 3 AND 5
AND e.JOB <> 'PRESIDENT'
AND e.SAL > (SELECT MAX(SAL) FROM EMPY JOIN DEPT ON EMPY.DEPTNO = DEPT.DEPTNO WHERE LOC = 'CHICAGO')
AND e.EMPNO IN (SELECT EMPNO FROM EMPY WHERE JOB IN ('MANAGER','SALESMAN') AND MGR IS NOT NULL AND MGR <> (SELECT EMPNO FROM EMPY WHERE ENAME='KING'))
;

```

**67. List the details of the senior employee belongs to 1981.**

```sql
-- Method 1: Using a Subquery
SELECT DISTINCT *FROM EMPY
WHERE HIREDATE = (SELECT MIN(HIREDATE) FROM EMPY WHERE YEAR(HIREDATE) = 1981);

-- Method 2: Using ORDER BY and LIMIT
SELECT DISTINCT * FROM EMPY
WHERE YEAR(HIREDATE) = 1981
ORDER BY HIREDATE ASC LIMIT 1;
```

**68. List the employees who joined in 1981 with the job same as the most senior person of the year 1981.**

```sql
-- Method 1: Using nested subqueries
SELECT DISTINCT * FROM EMPY
WHERE YEAR(HIREDATE) = 1981
AND JOB = (SELECT DISTINCT JOB FROM EMPY WHERE HIREDATE = (SELECT MIN(HIREDATE) FROM EMPY WHERE YEAR(HIREDATE) = 1981));

-- Method 2: Using a join
SELECT DISTINCT e1.* FROM EMPY e1
JOIN (SELECT JOB, MIN(HIREDATE) as min_date FROM EMPY WHERE YEAR(HIREDATE) = 1981 GROUP BY JOB) AS subquery
ON e1.JOB = subquery.JOB
WHERE YEAR(e1.HIREDATE) = 1981
AND e1.HIREDATE = subquery.min_date;

```

**69. List the most senior emp working under the king and grade is more than 3.**

```sql
-- Method 1: Using subquery
SELECT *
FROM EMPY
WHERE MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'KING')
AND GRADE > 3
ORDER BY HIREDATE ASC LIMIT 1;

-- Method 2: Using subquery and MAX function
SELECT *
FROM EMPY
WHERE MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'KING')
AND GRADE > 3
AND HIREDATE = (SELECT MIN(HIREDATE) FROM EMPY WHERE MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'KING') AND GRADE > 3 );
```

**70. Find the total sal given to the MGR.**

```sql
-- Method 1: Using SUM and WHERE
SELECT SUM(SAL) AS total_manager_salary
FROM EMPY
WHERE JOB = 'MANAGER';

-- Method 2: using sum with a subquery
SELECT SUM(SAL)
FROM (SELECT * FROM EMPY WHERE JOB = 'MANAGER') as subquery;
```

**71. Find the total annual sal to distribute job wise in the year 81.**

```sql
-- Method 1: Using GROUP BY and SUM
SELECT JOB, SUM(SAL * 12) AS total_annual_salary
FROM EMPY
WHERE YEAR(HIREDATE) = 1981
GROUP BY JOB;

-- Method 2: using subquery
SELECT JOB, SUM(annual_salary) as total_annual_salary
FROM(SELECT JOB,SAL*12 AS annual_salary
FROM EMPY
WHERE YEAR(HIREDATE) = 1981) AS subquery
GROUP BY JOB;
```

**72. Display total sal employee belonging to grade 3.**

```sql
-- Method 1: Using SUM and WHERE
SELECT SUM(SAL) AS total_salary_grade3
FROM EMPY
WHERE GRADE = 3;

-- Method 2: using sum with subquery
SELECT SUM(SAL) from (SELECT * FROM EMPY WHERE GRADE = 3) as subquery;
```

**73. Display the average salaries of all the clerks.**

```sql
-- Method 1: Using AVG and WHERE
SELECT AVG(SAL) AS average_clerk_salary
FROM EMPY
WHERE JOB = 'CLERK';

-- Method 2: Using subquery
SELECT AVG(SAL)
FROM (SELECT * FROM EMPY WHERE JOB = 'CLERK') as subquery;
```

**74. List the employee in dept 20 whose sal is > the average sal of dept 10 emps.**

```sql
-- Method 1: Using a Subquery
SELECT *
FROM EMPY
WHERE DEPTNO = 20
AND SAL > (SELECT AVG(SAL) FROM EMPY WHERE DEPTNO = 10);

-- Method 2: Using join
SELECT e1.*
FROM EMPY e1
JOIN (SELECT AVG(SAL) as avg_sal FROM EMPY WHERE DEPTNO=10) as subquery
ON e1.SAL > subquery.avg_sal
WHERE e1.DEPTNO = 20;

```

**75. Display the number of employee for each job group deptno wise.**

```sql
-- Method 1: Using GROUP BY and COUNT
SELECT DEPTNO, JOB, COUNT(*) AS number_of_employees
FROM EMPY
GROUP BY DEPTNO, JOB order by DEPTNO ;

-- Method 2: Using subquery (same logic but in a subquery)
SELECT DEPTNO, JOB, COUNT(*) AS number_of_employees
FROM (SELECT DEPTNO, JOB FROM EMPY) as subquery
GROUP BY DEPTNO, JOB  order by DEPTNO ;
```

**76. List the manager no and the number of employees working for those mgrs in the ascending Mgrno.**

```sql
-- Method 1: Using GROUP BY, COUNT and ORDER BY
SELECT MGR, COUNT(*) AS number_of_employees
FROM EMPY
WHERE MGR IS NOT NULL
GROUP BY MGR
ORDER BY MGR ASC;

-- Method 2 : USING subquery (same logic)
SELECT MGR, COUNT(*) AS number_of_employees
FROM (SELECT MGR FROM EMPY WHERE MGR IS NOT NULL) AS subquery
GROUP BY MGR
ORDER BY MGR ASC;
```

**77. List the department details where at least two emps are working.**

```sql
-- Method 1: Using HAVING clause
SELECT d.LOC, D.DNAME, D.DEPTNO
FROM DEPT d
JOIN EMPY e ON d.DEPTNO = e.DEPTNO
GROUP BY d.LOC, D.DNAME, D.DEPTNO
HAVING COUNT(*) >= 2;


-- Method 2: Using subquery
SELECT d.*
FROM DEPT d
JOIN (SELECT DEPTNO, COUNT(*) as emp_count FROM EMPY GROUP BY DEPTNO) AS emp_counts
ON d.DEPTNO = emp_counts.DEPTNO
WHERE emp_counts.emp_count >= 2;
```

**78. Display the Grade, Number of emps, and max sal of each grade.**

```sql
-- Method 1: Using GROUP BY and Aggregate Functions
SELECT GRADE, COUNT(*) AS number_of_employees, MAX(SAL) AS max_salary
FROM EMPY
GROUP BY GRADE;

-- Method 2: Using subquery
SELECT GRADE, COUNT(*) AS number_of_employees, MAX(SAL) AS max_salary
FROM (SELECT GRADE, SAL FROM EMPY) as subquery
GROUP BY GRADE;
```

**79. Display dname, grade, No. of emps where at least two emps are clerks.**

```sql
-- Method 1: Using Having and Group By
SELECT d.DNAME, e.GRADE, COUNT(*) AS num_of_emps
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.JOB = 'CLERK'
GROUP BY d.DNAME, e.GRADE
HAVING COUNT(*) >= 2;

-- Method 2: Using subquery and having
SELECT d.DNAME, e.GRADE, COUNT(*) AS num_of_emps
FROM (SELECT * FROM EMPY WHERE JOB='CLERK') AS e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
GROUP BY d.DNAME, e.GRADE
HAVING COUNT(*) >= 2;
```

**80. List the details of the department where maximum number of emps are working.**

```sql
-- Method 1: Using Subquery and LIMIT
SELECT d.DEPTNO,  COUNT(*) AS NO_OF_EMPS
FROM DEPT d
JOIN EMPY e ON d.DEPTNO = e.DEPTNO
GROUP BY d.DEPTNO
ORDER BY COUNT(*) DESC
LIMIT 1;

-- Method 2: Using a Common Table Expression (CTE)
WITH DeptEmpCounts AS (
    SELECT d.DEPTNO, d.DNAME, d.LOC, COUNT(*) AS emp_count
    FROM DEPT d
    JOIN EMPY e ON d.DEPTNO = e.DEPTNO
    GROUP BY d.DEPTNO, d.DNAME, d.LOC
)
SELECT DEPTNO, DNAME, LOC
FROM DeptEmpCounts
WHERE emp_count = (SELECT MAX(emp_count) FROM DeptEmpCounts);
```

**81. Display the emps whose manager name is jones.**

```sql
-- Method 1: Using Self-Join
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e2.ENAME = 'JONES';

-- Method 2 : USING a subquery
SELECT *
FROM EMPY
WHERE MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'JONES');
```

**82. List the employees whose salary is more than 3000 after giving 20% increment.**

```sql
-- Method 1:  Basic Calculation in WHERE Clause
SELECT *
FROM EMPY
WHERE SAL * 1.20 > 3000;

-- Method 2:  Using  Calculation in subquery (same logic)
SELECT *
FROM (SELECT *, SAL * 1.20 as incremented_sal FROM EMPY) AS subquery
WHERE incremented_sal > 3000;
```

**83. List the emps with dept names.**

```sql
-- Method 1:  Using basic join
SELECT DISTINCT e.*, d.DNAME
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO;

-- Method 2: using subquery (same logic)
SELECT  DISTINCT e.*, (SELECT DNAME FROM DEPT WHERE DEPTNO = e.DEPTNO) as dept_name
FROM EMPY e;
```

**84. List the emps who are not working in sales dept.**

```sql
-- Method 1: Using subquery and NOT IN
SELECT *
FROM EMPY
WHERE DEPTNO NOT IN (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES');

-- Method 2: Using join
SELECT e.*
FROM EMPY e
LEFT JOIN DEPT d ON e.DEPTNO = d.DEPTNO AND d.DNAME = 'SALES'
WHERE d.DEPTNO IS NULL;
```

**85. List the emps name, dept, sal and comm. For those whose salary is between 2000 and 5000 while loc is Chicago.**

```sql
-- Method 1: Using basic joins and conditions
SELECT DISTINCT  e.ENAME, d.DNAME, e.SAL, e.COMM
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.SAL BETWEEN 2000 AND 5000
AND d.LOC = 'CHICAGO';

-- Method 2: using subquery
SELECT DISTINCT  ENAME, (SELECT DNAME FROM DEPT WHERE DEPTNO = e.DEPTNO), SAL, COMM
FROM EMPY e
WHERE SAL BETWEEN 2000 AND 5000
AND DEPTNO = (SELECT DEPTNO FROM DEPT WHERE LOC='CHICAGO');
```

**86. List the emps whose sal is greater than his managers salary**

```sql
-- Method 1: Using Self-Join
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e1.SAL > e2.SAL;

-- Method 2 : Using subquery (same logic)
SELECT e1.*
FROM EMPY e1
WHERE e1.SAL > (SELECT SAL FROM EMPY WHERE EMPNO= e1.MGR);

```

**87. List the grade, EMP name for the deptno 10 or deptno 30 but sal grade is not 4 while they joined the company before ’31-dec- 82’.**

```sql
-- Method 1: Using OR and AND condition
SELECT GRADE, ENAME
FROM EMPY
WHERE (DEPTNO = 10 OR DEPTNO = 30)
AND GRADE <> 4
AND HIREDATE < '1982-12-31';

-- Method 2: Using In clause
SELECT GRADE, ENAME
FROM EMPY
WHERE DEPTNO IN (10,30)
AND GRADE <> 4
AND HIREDATE < '1982-12-31';
```

**88. List the name, job, dname, location for those who are working as MGRS.**

```sql
-- Method 1: Using basic joins and conditions
SELECT e.ENAME, e.JOB, d.DNAME, d.LOC
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.JOB = 'MANAGER';

-- Method 2 : Using subquery (same logic)
SELECT ENAME, JOB, (SELECT DNAME FROM DEPT WHERE DEPTNO = e.DEPTNO), (SELECT LOC FROM DEPT WHERE DEPTNO = e.DEPTNO)
FROM EMPY e
WHERE JOB = 'MANAGER';
```

**89. List the emps whose mgr name is jones and also list their manager name.**

```sql
-- Method 1: Using Self-Join
SELECT e1.ENAME AS employee_name, e2.ENAME AS manager_name
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e2.ENAME = 'JONES';

-- Method 2 : Using subquery (same logic)
SELECT ENAME AS employee_name, (SELECT ENAME from EMPY WHERE EMPNO= e.MGR ) AS manager_name
FROM EMPY e
WHERE MGR = (SELECT EMPNO FROM EMPY WHERE ENAME = 'JONES');
```

**90. List the name and salary of ford if his salary is equal to his sal of his grade.**


```sql
-- Method 1: Using self-join and a subquery
SELECT e1.ENAME, e1.SAL
FROM EMPY e1
WHERE e1.ENAME = 'FORD'
AND e1.SAL IN (SELECT SAL FROM EMPY WHERE GRADE = (SELECT GRADE FROM EMPY WHERE ENAME = 'FORD'));

-- Method 2: Using Subquery with IN clause
SELECT ENAME, SAL
FROM EMPY
WHERE ENAME = 'FORD'
AND SAL IN (SELECT SAL FROM EMPY WHERE GRADE = (SELECT GRADE FROM EMPY WHERE ENAME = 'FORD'));
```

**91. List the name, job, dname, sal, grade dept wise**

```sql
-- Method 1: Using JOIN and ORDER BY
SELECT  DISTINCT e.ENAME, e.JOB, d.DNAME, e.SAL, e.GRADE
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
ORDER BY e.DEPTNO;

-- Method 2: Using Subquery (same logic)
SELECT  DISTINCT  e.ENAME, e.JOB, (SELECT DNAME FROM DEPT WHERE DEPTNO = e.DEPTNO), e.SAL, e.GRADE
FROM EMPY e
ORDER BY e.DEPTNO;
```

**92. List the emp name, job, sal, grade and dname except clerks and sort on the basis of highest sal.**

```sql
-- Method 1: Using JOIN, WHERE, ORDER BY
SELECT DISTINCT  e.ENAME, e.JOB, e.SAL, e.GRADE, d.DNAME
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.JOB <> 'CLERK'
ORDER BY e.SAL DESC;

-- Method 2: Using subquery (same logic)
SELECT  DISTINCT e.ENAME, e.JOB, e.SAL, e.GRADE, (SELECT DNAME FROM DEPT WHERE DEPTNO=e.DEPTNO)
FROM EMPY e
WHERE e.JOB <> 'CLERK'
ORDER BY e.SAL DESC;

```

**93. List the emps name, job who are without manager.**

```sql
-- Method 1: Using WHERE clause with IS NULL
SELECT ENAME, JOB
FROM EMPY
WHERE MGR IS NULL;

-- Method 2: Using ISNULL Function (some DBs have this instead)
SELECT ENAME, JOB
FROM EMPY
WHERE ISNULL(MGR);
```

**94. List the names of the emps who are getting the highest sal dept wise.**

```sql
-- Method 1: Using subquery with IN
SELECT e1.ENAME
FROM EMPY e1
WHERE (e1.DEPTNO, e1.SAL) IN (
    SELECT e2.DEPTNO, MAX(e2.SAL)
    FROM EMPY e2
    GROUP BY e2.DEPTNO
);

-- Method 2: Using a Self Join and Subquery
SELECT e1.ENAME
FROM EMPY e1
JOIN (SELECT DEPTNO, MAX(SAL) as max_sal FROM EMPY GROUP BY DEPTNO) AS max_sal_dept
ON e1.DEPTNO = max_sal_dept.DEPTNO AND e1.SAL = max_sal_dept.max_sal;
```

**95. List the emps whose sal is equal to the average of max and minimum.**

```sql
-- Method 1: Using a subquery for the average
SELECT *
FROM EMPY
WHERE SAL = (
    SELECT (MAX(SAL) + MIN(SAL)) / 2
    FROM EMPY
);

-- Method 2: Using Variables (less portable, but works in some systems like MySQL)
SELECT * FROM EMPY WHERE SAL = ((SELECT MAX(SAL) FROM EMPY) + (SELECT MIN(SAL) FROM EMPY)) / 2;
```

**96. List the no. of emps in each department where the no. is more than 3.**

```sql
-- Method 1: Using GROUP BY and HAVING clause
SELECT DEPTNO, COUNT(*) AS number_of_employees
FROM EMPY
GROUP BY DEPTNO
HAVING COUNT(*) > 3;

-- Method 2: using subquery (same logic)
SELECT DEPTNO, COUNT(*) AS number_of_employees
FROM (SELECT DEPTNO FROM EMPY) AS subquery
GROUP BY DEPTNO
HAVING COUNT(*) > 3;
```

**97. List the names of depts. Where at least 3 are working in that department.**

```sql
-- Method 1: Using JOIN, GROUP BY and HAVING
SELECT d.DNAME
FROM DEPT d
JOIN EMPY e ON d.DEPTNO = e.DEPTNO
GROUP BY d.DNAME
HAVING COUNT(*) >= 3;

-- Method 2: using subquery (same logic)
SELECT DNAME
FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMPY GROUP BY DEPTNO HAVING COUNT(*) >= 3);
```

**98. List the managers whose sal is more than his employees avg salary.**

```sql
-- Method 1: Using Self-Join and Subquery
SELECT e1.*
FROM EMPY e1
WHERE e1.JOB = 'MANAGER'
AND e1.SAL > (
    SELECT AVG(SAL)
    FROM EMPY e2
    WHERE e2.MGR = e1.EMPNO
);

-- Method 2: Using Join and Group By
SELECT e1.*
FROM EMPY e1
JOIN (SELECT MGR, AVG(SAL) as avg_salary FROM EMPY GROUP BY MGR) AS subquery
ON e1.EMPNO = subquery.MGR
WHERE e1.JOB = 'MANAGER' and e1.SAL > subquery.avg_salary;
```

**99. List the name,salary,comm. For those employees whose net pay is greater than or equal to any other employee salary of the company.**

```sql
-- Method 1: Using Subquery and MAX with  IFNULL()
SELECT ENAME, SAL, COMM
FROM EMPY
WHERE (SAL + IFNULL(COMM, 0)) >= ALL (SELECT (SAL + IFNULL(COMM,0)) FROM EMPY);


-- Method 2: Using ORDER BY and LIMIT 1
SELECT ENAME, SAL, COMM FROM EMPY
ORDER BY (SAL + IFNULL(COMM, 0)) DESC LIMIT 1;
```

**100. List the emp whose sal < his manager but more than any other manager.**

```sql
-- Method 1: Using Nested Subqueries
SELECT e1.*
FROM EMPY e1
WHERE e1.SAL < (SELECT SAL FROM EMPY WHERE EMPNO = e1.MGR)
AND e1.SAL > ALL (SELECT SAL FROM EMPY WHERE JOB = 'MANAGER');

-- Method 2: Using Join and All clause
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e1.MGR = e2.EMPNO
WHERE e1.SAL < e2.SAL
AND e1.SAL > ALL (SELECT SAL FROM EMPY WHERE JOB = 'MANAGER');
```
