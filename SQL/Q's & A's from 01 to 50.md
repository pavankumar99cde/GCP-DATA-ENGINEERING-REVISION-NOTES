
---

1. **Display all the information of the EMP table**

```sql
-- Method 1
SELECT * FROM EMPY;
-- Method 2
SELECT EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO, GRADE FROM EMPY;
```

---

2. **Display unique Jobs from EMP table**

```sql
-- Method 1
SELECT DISTINCT JOB FROM EMPY;
-- Method 2
SELECT JOB FROM EMPY GROUP BY JOB;
```

---

3. **List the employees in the ascending order of their Salaries**

```sql
-- Method 1
SELECT * FROM EMPY ORDER BY SAL ASC;
-- Method 2
SELECT * FROM EMPY ORDER BY SAL;
```

---

4. **List the details of the employees in ascending order of Deptnos and descending order of Jobs**

```sql
-- Method 1
SELECT * FROM EMPY ORDER BY DEPTNO ASC, JOB DESC;
-- Method 2
SELECT * FROM EMPY ORDER BY DEPTNO, JOB DESC;
```

---

5. **Display all the unique job groups in the descending order**

```sql
-- Method 1
SELECT JOB FROM EMPY GROUP BY JOB ORDER BY COUNT(JOB) DESC;
-- Method 2
SELECT JOB FROM EMPY GROUP BY JOB ORDER BY JOB DESC;
```

---

6. **Display all the details of all ‘Mgrs’**

```sql
-- Method 1
SELECT DISTINCT MGR FROM EMPY;
-- Method 2
SELECT JOB FROM EMPY GROUP BY JOB;
```

---

7. **List the employees who joined before 1981**

```sql
-- Method 1
SELECT * FROM EMPY WHERE YEAR(HIREDATE) < 1981;
-- Method 2
SELECT * FROM EMPY WHERE HIREDATE < '1981-01-01';
```

---

8. **List the Empno, Ename, Sal, Daily sal of all employees in the ascending order of Annual Salary**

```sql
-- Method 1
SELECT EMPNO, ENAME, SAL, SAL / 30 AS DAILY_SAL, SAL * 365 AS ANNUAL_SAL 
FROM EMPY 
ORDER BY ANNUAL_SAL ASC;

```

---

9. **Display the Empno, Ename, job, Hiredate, Exp of all Managers**

```sql
-- Method 1
SELECT EMPNO, ENAME, JOB, HIREDATE, YEAR(CURRENT_DATE()) - YEAR(HIREDATE) AS EXP FROM EMPY WHERE JOB = 'MANAGER';
-- Method 2
SELECT EMPNO, ENAME, JOB, HIREDATE, DATEDIFF(CURRENT_DATE(), HIREDATE) / 365 AS EXP FROM EMPY WHERE JOB = 'MANAGER';
```

---

10. **List the Empno, Ename, Sal, Exp of all employees working for Manager 7369**

```sql

-- Method 1
SELECT EMPNO, ENAME, SAL, YEAR(CURRENT_DATE()) - YEAR(HIREDATE) AS EXP FROM EMPY WHERE MGR = 7369;
```

---

11. **Display all the details of the employees whose Comm. is more than their Sal**

```sql
-- Method 1
SELECT * FROM EMPY WHERE COMM > SAL;
-- Method 2
SELECT * FROM EMPY WHERE (COMM IS NOT NULL) AND COMM > SAL;
```

---

12. **List the employees in the ascending order of Designations of those who joined after the second half of 1981**

```sql
-- Method 1
SELECT ENAME, JOB FROM EMPY WHERE YEAR(HIREDATE) > 1981 AND MONTH(HIREDATE) > 6 ORDER BY JOB ASC;
-- Method 2
SELECT ENAME, JOB FROM EMPY WHERE HIREDATE > '1981-06-30' ORDER BY JOB ASC;
```

---

13. **List the employees along with their Exp and Daily Sal greater than Rs.100**

```sql
-- Method 1
SELECT *, YEAR(CURRENT_DATE()) - YEAR(HIREDATE) AS EXP FROM EMPY WHERE SAL / 30 > 100;
-- Method 2
SELECT *, DATEDIFF(CURRENT_DATE(), HIREDATE) / 365 AS EXP FROM EMPY WHERE SAL / 30 > 100;
```

---

14. **List the employees who are either ‘CLERK’ or ‘ANALYST’ in descending order**

```sql
-- Method 1
SELECT * FROM EMPY WHERE JOB = 'CLERK' OR JOB = 'ANALYST' ORDER BY JOB DESC;
-- Method 2
SELECT * FROM EMPY WHERE JOB IN ('CLERK', 'ANALYST') ORDER BY JOB DESC;
```

---

15. **List the employees who joined on 1-MAY-81, 3-DEC-81, 17-DEC-81, 19-JAN-80 in ascending order of seniority**

```sql
-- Method 1
SELECT * FROM EMPY WHERE DATE_FORMAT(HIREDATE, '%d-%b-%y') IN ('01-MAY-81', '03-DEC-81', '17-DEC-81', '19-JAN-80') ORDER BY HIREDATE ASC;
-- Method 2
SELECT * FROM EMPY WHERE HIREDATE IN ('1981-05-01', '1981-12-03', '1981-12-17', '1980-01-19') ORDER BY HIREDATE ASC;
```

---

16. **List the employees who are working for Deptno 10 or 20**

```sql
-- Method 1
SELECT * FROM EMPY WHERE DEPTNO IN (10, 20);
-- Method 2
SELECT * FROM EMPY WHERE DEPTNO = 10 OR DEPTNO = 20;
```

---

17. **List the employees who joined in the year 81**

```sql
-- Method 1
SELECT * FROM EMPY WHERE YEAR(HIREDATE) = 1981;
-- Method 2
SELECT * FROM EMPY WHERE HIREDATE BETWEEN '1981-01-01' AND '1981-12-31';
```

---

18. **List the employees who joined in the month of August 1980**

```sql
-- Method 1
SELECT *, DATE_FORMAT(HIREDATE, '%e-%b-%Y') FROM EMPY WHERE MONTH(HIREDATE) = 8 AND YEAR(HIREDATE) = 1980;
-- Method 2
SELECT *, DATE_FORMAT(HIREDATE, '%e-%b-%Y') FROM EMPY WHERE HIREDATE BETWEEN '1980-08-01' AND '1980-08-31';
```

---

19. **List the employees whose annual salary ranges from 220000 and 450000**

```sql
-- Method 1
SELECT *, SAL * 12 AS ANNUAL_SAL FROM EMPY WHERE SAL * 12 BETWEEN 220000 AND 450000;
```

---

20. **List the employees whose names have exactly five characters**

```sql
-- Method 1
SELECT ENAME FROM EMPY WHERE ENAME LIKE '_____';
-- Method 2
SELECT ENAME FROM EMPY WHERE LENGTH(ENAME) = 5;
```

---

21. **List the employees whose names start with ‘S’ and have five characters**

```sql
-- Method 1
SELECT ENAME FROM EMPY WHERE ENAME LIKE 'S____';
-- Method 2
SELECT ENAME FROM EMPY WHERE ENAME LIKE 'S%' AND LENGTH(ENAME) = 5;
```

---

22. **List the employees whose names have four characters and the third character is ‘r’**

```sql
-- Method 1
SELECT ENAME FROM EMPY WHERE ENAME LIKE '___r';
-- Method 2
SELECT ENAME FROM EMPY WHERE LENGTH(ENAME) = 4 AND SUBSTRING(ENAME, 3, 1) = 'r';
```

---

23. **List the five character names starting with ‘S’ and ending with ‘H’**

```sql
-- Method 1
SELECT ENAME FROM EMPY WHERE ENAME LIKE 'S___H';
-- Method 2
SELECT ENAME FROM EMPY WHERE ENAME LIKE 'S%H' AND LENGTH(ENAME) = 5;
```

---

24. **List the employees who joined in January**

```sql
-- Method 1
SELECT * FROM EMPY WHERE DATE_FORMAT(HIREDATE, '%M') = 'January';
-- Method 2
SELECT * FROM EMPY WHERE MONTH(HIREDATE) = 1;
```

---

25. **List the employees who joined in the month whose second character is ‘a’**

```sql
-- Method 1
SELECT * , DATE_FORMAT(HIREDATE, '%M') AS MONTHS FROM EMPY WHERE DATE_FORMAT(HIREDATE, '%M') LIKE '_a%';
-- Method 2
SELECT * FROM EMPY WHERE MONTHNAME(HIREDATE) LIKE '_a%';
```

---

26. **List the employees whose salary is a four-digit number ending with zero**

```sql
-- Method 1
SELECT ENAME FROM EMPY WHERE SAL LIKE '___0';
-- Method 2
SELECT ENAME FROM EMPY WHERE SAL % 10 = 0 AND SAL BETWEEN 1000 AND 9999;
```

---

27. **List the employees whose names contain the character set ‘ll’ together**

```sql
-- Method 1
SELECT * FROM EMPY WHERE ENAME LIKE '%ll%';
-- Method 2
SELECT * FROM EMPY WHERE ENAME REGEXP 'll';
```

---

28. **List the employees who joined in the 1980s**

```sql
-- Method 1
SELECT * FROM EMPY WHERE YEAR(HIREDATE) BETWEEN 1980 AND 1989;
-- Method 2
SELECT * FROM EMPY WHERE HIREDATE >= '1980-01-01' AND HIREDATE < '1990-01-01';
```

---

29. **List the employees who do not belong to Deptno 20**

```sql
-- Method 1
SELECT * FROM EMPY WHERE DEPTNO != 20;
-- Method 2
SELECT * FROM EMPY WHERE DEPTNO <> 20;
```

---

30. **List all the employees except ‘PRESIDENT’ & ‘MGR’ in ascending order of Salaries**

```sql
-- Method 1
SELECT * FROM EMPY WHERE JOB NOT IN ('PRESIDENT', 'MANAGER') ORDER BY SAL ASC;
-- Method 2
SELECT * FROM EMPY WHERE JOB <> 'PRESIDENT' AND JOB <> 'MANAGER' ORDER BY SAL ASC;
```


---

### 31. List all the employees who joined before or after 1981.

```sql
-- Method 1
SELECT * FROM EMPY WHERE YEAR(HIREDATE) != 1981;

-- Method 2
SELECT * FROM EMPY WHERE HIREDATE < '1981-01-01' OR HIREDATE > '1981-12-31';
```

---

### 32. List the employees whose Empno does not start with digit 78.

```sql
-- Method 1
SELECT * FROM EMPY WHERE EMPNO NOT LIKE '78%';

-- Method 2
SELECT * FROM EMPY WHERE LEFT(EMPNO, 2) != '78';
```

---

### 33. List the employees who are working under 'MGR'.

```sql
-- Method 1
SELECT E1.EMPNO AS Empno, E1.ENAME AS EmpName, E2.ENAME AS Manager 
FROM EMPY AS E1
INNER JOIN EMPY AS E2 ON E1.MGR = E2.EMPNO;

-- Method 2
SELECT * FROM EMPY WHERE MGR IS NOT NULL;
```

---

### 34. List the employees who joined in any year but not in March.

```sql
-- Method 1
SELECT * FROM EMPY WHERE MONTH(HIREDATE) != 3;

-- Method 2
SELECT * FROM EMPY WHERE HIREDATE NOT LIKE '__-03-%';
```

---

### 35. List all the Clerks of Deptno 20.

```sql
-- Method 1
SELECT * FROM EMPY WHERE JOB = 'CLERK' AND DEPTNO = 20;

-- Method 2
SELECT * FROM EMPY WHERE JOB = 'CLERK' AND DEPTNO IN (20);
```

---

### 36. List the employees of Deptno 30 or 10 who joined in the year 1981.

```sql
-- Method 1
SELECT * FROM EMPY WHERE YEAR(HIREDATE) = 1981 AND DEPTNO IN (10, 30);

-- Method 2
SELECT * FROM EMPY WHERE DEPTNO = 30 OR DEPTNO = 10 AND YEAR(HIREDATE) = 1981;
```

---

### 37. Display the details of SMITH.

```sql
-- Method 1
SELECT * FROM EMPY WHERE ENAME = 'SMITH';

-- Method 2
SELECT * FROM EMPY WHERE LOWER(ENAME) = 'smith';
```

---

### 38. Display the location of SMITH.

```sql
-- Method 1
SELECT D.LOC 
FROM EMPY E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE E.ENAME = 'SMITH';

-- Method 2
SELECT LOC 
FROM DEPT 
WHERE DEPTNO = (SELECT DEPTNO FROM EMPY WHERE ENAME = 'SMITH');
```

---

### 39. List the total information of EMP table along with DNAME and LOC of all the employees working under 'ACCOUNTING' and 'RESEARCH'.

```sql
-- Method 1
SELECT E.*, D.DNAME, D.LOC 
FROM EMPY E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME IN ('ACCOUNTING', 'RESEARCH')
ORDER BY E.DEPTNO ASC;

-- Method 2
SELECT * FROM EMPY 
JOIN DEPT ON EMPY.DEPTNO = DEPT.DEPTNO 
WHERE DNAME = 'ACCOUNTING' OR DNAME = 'RESEARCH';
```

---

### 40. List the Empno, Ename, Sal, Dname of all the 'MGRS' and 'ANALYST' working in New York, Dallas with experience more than 7 years without receiving Comm, sorted by location.

```sql
-- Method 1
SELECT E.EMPNO, E.ENAME, E.SAL, D.DNAME 
FROM EMPY E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE (D.LOC IN ('NEW YORK', 'DALLAS')) 
  AND (YEAR(CURRENT_DATE()) - YEAR(E.HIREDATE)) > 7 
  AND E.COMM IS NULL 
ORDER BY D.LOC ASC;

-- Method 2
SELECT EMPNO, ENAME, SAL, DNAME 
FROM EMPY E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE D.LOC = 'NEW YORK' OR D.LOC = 'DALLAS'
  AND (YEAR(CURRENT_DATE()) - YEAR(HIREDATE)) > 7
  AND COMM IS NULL;

Here are your edited SQL queries in the requested format:

---

**41. Display the Empno, Ename, Sal, Dname, Loc, Deptno, Job of all emps working at CHICAGO or working for ACCOUNTING dept with Ann Sal>280000, but the Sal should not be=3000 or 2800 who doesn’t belong to the Mgr and whose no is having a digit ‘7’ or ‘8’ in 3rd position in the asc order of Deptno and desc order of job.**

```sql
-- Method 1: Using OR and LIKE for combined condition
SELECT e.EMPNO, e.ENAME, e.SAL, d.DNAME, d.LOC, e.DEPTNO, e.JOB
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE (d.LOC = 'CHICAGO' OR (d.DNAME = 'ACCOUNTING' AND e.SAL*12 > 280000))
AND e.SAL NOT IN (3000,2800)
AND e.JOB <> 'MANAGER'
AND (SUBSTR(CAST(e.EMPNO AS CHAR), 3, 1) IN ('7', '8'))
ORDER BY e.DEPTNO ASC, e.JOB DESC;

-- Method 2: Using UNION to separate conditions and then combine
SELECT e.EMPNO, e.ENAME, e.SAL, d.DNAME, d.LOC, e.DEPTNO, e.JOB
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE d.LOC = 'CHICAGO' 
AND e.SAL NOT IN (3000,2800)
AND e.JOB <> 'MANAGER'
AND (SUBSTR(CAST(e.EMPNO AS CHAR), 3, 1) IN ('7', '8'))
UNION
SELECT e.EMPNO, e.ENAME, e.SAL, d.DNAME, d.LOC, e.DEPTNO, e.JOB
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE d.DNAME = 'ACCOUNTING' AND e.SAL*12 > 280000
AND e.SAL NOT IN (3000,2800)
AND e.JOB <> 'MANAGER'
AND (SUBSTR(CAST(e.EMPNO AS CHAR), 3, 1) IN ('7', '8'))
ORDER BY DEPTNO ASC, JOB DESC;
```

---

**42. Display the total information of the emps along with Grades in the asc order.**

```sql
-- Method 1
SELECT DISTINCT * FROM EMPY ORDER BY GRADE ASC;
```

---

**43. List all the Grade2 and Grade 3 emps.**

```sql
-- Method 1
SELECT DISTINCT * FROM EMPY WHERE GRADE IN (2, 3);

-- Method 2
SELECT DISTINCT * FROM EMPY WHERE GRADE = 2 OR GRADE = 3;
```

---

**44. Display all Grade 4,5 Analyst and Mgr.**

```sql
-- Method 1
SELECT * FROM EMPY WHERE GRADE = 4 OR GRADE = 5 AND JOB IN ('ANALYST','MANAGER');

-- Method 2
SELECT * FROM EMPY WHERE (GRADE = 4 OR GRADE = 5) AND JOB = 'ANALYST' OR JOB = 'MANAGER';
```

---

**45. List the Empno, Ename, Sal, Dname, Grade, Exp, and AnnSal of emps working for Dept10 or20.**

```sql
-- Method 1
SELECT e.EMPNO, e.ENAME, e.SAL, d.DNAME, e.GRADE, YEAR(CURDATE())-YEAR(e.HIREDATE) AS EXP, e.SAL*12 as AnnSal
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.DEPTNO IN (10, 20);

-- Method 2
SELECT e.EMPNO, e.ENAME, e.SAL, d.DNAME, e.GRADE, YEAR(CURDATE())-YEAR(e.HIREDATE) AS EXP, e.SAL*12 as AnnSal
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.DEPTNO = 10 OR e.DEPTNO = 20;
```

---

**46. List all the information of emp with Loc and the Grade of all the emps belong to the Grade range from 2 to 4 working at the Dept those are not starting with char set ‘OP’ and not ending with ‘S’ with the designation having a char ‘a’ any where joined in the year 1981 but not in the month of Mar or Sep and Sal not end with ‘00’ in the asc order of Grades.**

```sql
-- Method 1
SELECT e.*, d.LOC, e.GRADE
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.GRADE BETWEEN 2 AND 4
AND d.DNAME NOT LIKE 'OP%' AND d.DNAME NOT LIKE '%S'
AND e.JOB LIKE '%a%'
AND YEAR(e.HIREDATE) = 1981
AND MONTH(e.HIREDATE) NOT IN (3, 9)
AND e.SAL NOT LIKE '%00'
ORDER BY e.GRADE ASC;

-- Method 2
SELECT e.*, d.LOC, e.GRADE
FROM EMPY e
JOIN DEPT d ON e.DEPTNO = d.DEPTNO
WHERE e.GRADE BETWEEN 2 AND 4
AND d.DNAME NOT LIKE 'OP%' AND d.DNAME NOT LIKE '%S'
AND e.JOB LIKE '%a%'
AND YEAR(e.HIREDATE) = 1981
AND MONTH(e.HIREDATE) NOT IN (3, 9)
AND e.SAL NOT LIKE '%00'
ORDER BY e.GRADE ASC;
```

---

**47. List the details of the Depts along with Empno, Ename or without the emps.**

```sql
-- Method 1
SELECT DISTINCT e.EMPNO, e.ENAME , d.*
FROM DEPT d
LEFT JOIN EMPY e ON d.DEPTNO = e.DEPTNO;

-- Method 2
SELECT DISTINCT  d.*, e.EMPNO, e.ENAME
FROM EMPY e
RIGHT JOIN DEPT d ON d.DEPTNO = e.DEPTNO;
```

---

**48. List the details of the emps whose Salaries more than the employee BLAKE.**

```sql
-- Method 1 (Subquery)
SELECT * FROM EMPY WHERE SAL > (SELECT SAL FROM EMPY WHERE ENAME = 'BLAKE');

-- Method 2 (Self-Join)
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e2.ENAME = 'BLAKE'
WHERE e1.SAL > e2.SAL;
```

---

**49. List the emps whose Jobs are same as ALLEN.**

```sql
-- Method 1 (Subquery)
SELECT DISTINCT * FROM EMPY WHERE JOB = (SELECT DISTINCT JOB FROM EMPY WHERE ENAME = 'ALLEN');

-- Method 2 (Self-Join)
SELECT DISTINCT  e1.*
FROM EMPY e1
JOIN EMPY e2 ON e2.ENAME = 'ALLEN'
WHERE e1.JOB = e2.JOB;
```

---

**50. List the emps who are senior to King.**

```sql
-- Method 1 (Subquery)
SELECT DISTINCT *
FROM EMPY
WHERE HIREDATE < (SELECT HIREDATE FROM EMPY WHERE ENAME = 'KING');

-- Method 2 (Self-Join)
SELECT e1.*
FROM EMPY e1
JOIN EMPY e2 ON e2.ENAME = 'KING'
WHERE e1.HIREDATE < e2.HIREDATE;
```
