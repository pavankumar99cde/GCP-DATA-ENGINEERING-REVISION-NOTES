## 1. Difference between `WHERE`, `HAVING`, and `QUALIFY`

| Feature             | WHERE           | HAVING         | QUALIFY                    |
| ------------------- | --------------- | -------------- | -------------------------- |
| Filters             | Rows            | Groups         | Window function results    |
| Executes            | Before GROUP BY | After GROUP BY | After Window Functions     |
| Aggregate functions | ❌ Not allowed   | ✅ Allowed      | ❌ Not directly             |
| Window functions    | ❌ No            | ❌ No           | ✅ Yes                      |
| Used with           | SELECT          | GROUP BY       | ROW_NUMBER(), RANK(), etc. |

---

## 2. Difference between `DELETE`, `TRUNCATE`, and `DROP`

| Feature           | DELETE        | TRUNCATE      | DROP         |
| ----------------- | ------------- | ------------- | ------------ |
| Removes           | Selected rows | All rows      | Entire table |
| WHERE clause      | ✅ Yes         | ❌ No          | ❌ No         |
| Structure remains | ✅ Yes         | ✅ Yes         | ❌ No         |
| Rollback          | Usually Yes   | Depends on DB | Usually No   |
| Speed             | Slow          | Fast          | Fastest      |

---

## 3. Difference between `PRIMARY KEY`, `UNIQUE KEY`, and `FOREIGN KEY`

| Feature          | PRIMARY KEY           | UNIQUE KEY                 | FOREIGN KEY           |
| ---------------- | --------------------- | -------------------------- | --------------------- |
| Duplicate values | ❌ No                  | ❌ No                       | ✅ Yes                 |
| NULL allowed     | ❌ No                  | Usually Yes (DB dependent) | ✅ Yes                 |
| One per table    | ✅ Yes                 | Multiple                   | Multiple              |
| Purpose          | Unique row identifier | Enforce uniqueness         | Maintain relationship |

---

## 4. Difference between `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL OUTER JOIN`

| Join            | Returns                                   |
| --------------- | ----------------------------------------- |
| INNER JOIN      | Matching rows from both tables            |
| LEFT JOIN       | All left table rows + matching right rows |
| RIGHT JOIN      | All right table rows + matching left rows |
| FULL OUTER JOIN | All rows from both tables                 |

---

## 5. Difference between `UNION` and `UNION ALL`

| Feature                       | UNION  | UNION ALL |
| ----------------------------- | ------ | --------- |
| Removes duplicates            | ✅ Yes  | ❌ No      |
| Performance                   | Slower | Faster    |
| Sorting for duplicate removal | Yes    | No        |

---

## 6. Difference between `GROUP BY` and `ORDER BY`

| Feature                | GROUP BY        | ORDER BY   |
| ---------------------- | --------------- | ---------- |
| Purpose                | Groups rows     | Sorts rows |
| Changes number of rows | ✅ Yes           | ❌ No       |
| Aggregate functions    | Usually used    | Optional   |
| Execution              | Before ORDER BY | Last step  |

---

## 7. Difference between `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`

| Feature          | ROW_NUMBER() | RANK() | DENSE_RANK() |
| ---------------- | ------------ | ------ | ------------ |
| Duplicate ranks  | ❌ No         | ✅ Yes  | ✅ Yes        |
| Rank gaps        | ❌ No         | ✅ Yes  | ❌ No         |
| Every row unique | ✅ Yes        | ❌ No   | ❌ No         |

---

## 8. Difference between `RANK()` and `DENSE_RANK()`

| Feature                | RANK()  | DENSE_RANK() |
| ---------------------- | ------- | ------------ |
| Same values share rank | ✅ Yes   | ✅ Yes        |
| Rank skipped after tie | ✅ Yes   | ❌ No         |
| Example                | 1,2,2,4 | 1,2,2,3      |

---

## 9. Difference between `ROW_NUMBER()` and `RANK()`

| Feature          | ROW_NUMBER()        | RANK()    |
| ---------------- | ------------------- | --------- |
| Duplicate values | Different numbers   | Same rank |
| Rank gaps        | ❌ No                | ✅ Yes     |
| Best for         | Removing duplicates | Ranking   |

---

## 10. Difference between Aggregate Functions and Window Functions

| Feature       | Aggregate Function | Window Function            |
| ------------- | ------------------ | -------------------------- |
| Returns       | One row per group  | One row per input row      |
| Uses GROUP BY | Usually Yes        | No                         |
| Examples      | SUM(), COUNT()     | ROW_NUMBER(), SUM() OVER() |

---

## 11. Difference between `PARTITION BY` and `GROUP BY`

| Feature                | PARTITION BY     | GROUP BY          |
| ---------------------- | ---------------- | ----------------- |
| Used in                | Window Functions | Aggregate Queries |
| Original rows retained | ✅ Yes            | ❌ No              |
| Groups data            | Logically        | Physically        |

---

## 12. Difference between `DISTINCT` and `GROUP BY`

| Feature             | DISTINCT    | GROUP BY    |
| ------------------- | ----------- | ----------- |
| Removes duplicates  | ✅ Yes       | ✅ Yes       |
| Aggregate functions | ❌ No        | ✅ Yes       |
| Main purpose        | Unique rows | Aggregation |

---

## 13. Difference between `CHAR` and `VARCHAR`

| Feature     | CHAR               | VARCHAR       |
| ----------- | ------------------ | ------------- |
| Length      | Fixed              | Variable      |
| Storage     | Always full length | Actual length |
| Performance | Slightly faster    | Saves space   |

---

## 14. Difference between `CHAR`, `VARCHAR`, and `STRING`

| Feature   | CHAR           | VARCHAR        | STRING                |
| --------- | -------------- | -------------- | --------------------- |
| Length    | Fixed          | Variable       | Unlimited/Variable    |
| Storage   | Fixed          | Variable       | Variable              |
| Supported | Most databases | Most databases | BigQuery, Spark, etc. |

---

## 15. Difference between `NVL()`, `COALESCE()`, and `IFNULL()`

| Feature        | NVL()  | COALESCE() | IFNULL()        |
| -------------- | ------ | ---------- | --------------- |
| Arguments      | 2      | Multiple   | 2               |
| Standard SQL   | ❌ No   | ✅ Yes      | ❌ No            |
| Mainly used in | Oracle | Most DBs   | MySQL, BigQuery |

---

## 16. Difference between `CASE WHEN` and `IF()`

| Feature      | CASE WHEN | IF()    |
| ------------ | --------- | ------- |
| Conditions   | Multiple  | One     |
| Standard SQL | ✅ Yes     | ❌ No    |
| Readability  | Better    | Simpler |

---

## 17. Difference between `EXISTS`, `IN`, and `JOIN`

| Feature                 | EXISTS           | IN           | JOIN           |
| ----------------------- | ---------------- | ------------ | -------------- |
| Purpose                 | Check existence  | Match values | Combine tables |
| Returns columns         | ❌ No             | ❌ No         | ✅ Yes          |
| Stops after first match | ✅ Yes            | ❌ No         | ❌ No           |
| Best for                | Large subqueries | Small lists  | Fetching data  |

---

## 18. Difference between `EXISTS` and `IN`

| Feature                 | EXISTS                    | IN                        |
| ----------------------- | ------------------------- | ------------------------- |
| Performance             | Better for large datasets | Better for small datasets |
| Stops after first match | ✅ Yes                     | ❌ No                      |
| NULL handling           | Better                    | Can be tricky             |

---

## 19. Difference between Correlated Subquery and Non-Correlated Subquery

| Feature                | Correlated   | Non-Correlated |
| ---------------------- | ------------ | -------------- |
| Depends on outer query | ✅ Yes        | ❌ No           |
| Execution              | Once per row | Once           |
| Performance            | Slower       | Faster         |

---

## 20. Difference between Subquery and Common Table Expression (CTE)

| Feature     | Subquery | CTE    |
| ----------- | -------- | ------ |
| Readability | Lower    | Higher |
| Reusable    | ❌ No     | ✅ Yes  |
| Recursive   | ❌ No     | ✅ Yes  |

---

## 21. Difference between CTE and Temporary Table

| Feature           | CTE          | Temporary Table |
| ----------------- | ------------ | --------------- |
| Stored physically | ❌ No         | ✅ Yes           |
| Scope             | Single query | Session         |
| Indexes           | ❌ No         | ✅ Yes           |

---

## 22. Difference between View and Materialized View

| Feature        | View   | Materialized View |
| -------------- | ------ | ----------------- |
| Stores data    | ❌ No   | ✅ Yes             |
| Query speed    | Slower | Faster            |
| Refresh needed | No     | Yes               |

---

## 23. Difference between Clustered Index and Non-Clustered Index

| Feature       | Clustered Index          | Non-Clustered Index |
| ------------- | ------------------------ | ------------------- |
| Data order    | Physical                 | Logical             |
| One per table | ✅ Yes                    | Multiple            |
| Speed         | Faster for range queries | Faster for lookups  |

---

## 24. Difference between OLTP and OLAP

| Feature    | OLTP                   | OLAP                   |
| ---------- | ---------------------- | ---------------------- |
| Purpose    | Transactions           | Analytics              |
| Operations | INSERT, UPDATE, DELETE | Complex SELECT         |
| Data       | Current                | Historical             |
| Speed      | Very fast              | Optimized for analysis |

---

## 25. Difference between Normalization and Denormalization

| Feature     | Normalization | Denormalization |
| ----------- | ------------- | --------------- |
| Redundancy  | Less          | More            |
| Joins       | More          | Fewer           |
| Performance | Better writes | Better reads    |

---

## 26. Difference between `WHERE` clause and `ON` clause in a JOIN

| Feature          | WHERE                     | ON                       |
| ---------------- | ------------------------- | ------------------------ |
| Purpose          | Filter results            | Define join condition    |
| Applied          | After JOIN                | During JOIN              |
| LEFT JOIN impact | Can remove unmatched rows | Preserves unmatched rows |

---

## 27. Difference between Scalar Function and Aggregate Function

| Feature | Scalar Function   | Aggregate Function |
| ------- | ----------------- | ------------------ |
| Input   | One value         | Multiple rows      |
| Output  | One value         | One value          |
| Example | UPPER(), LENGTH() | SUM(), AVG()       |

---

## 28. Difference between Stored Procedure, Function, and Trigger

| Feature                | Stored Procedure | Function | Trigger |
| ---------------------- | ---------------- | -------- | ------- |
| Called manually        | ✅ Yes            | ✅ Yes    | ❌ No    |
| Returns value          | Optional         | Required | No      |
| Executes automatically | ❌ No             | ❌ No     | ✅ Yes   |

---

## 29. Difference between `NULL` and Empty String (`''`)

| Feature    | NULL            | Empty String (`''`) |
| ---------- | --------------- | ------------------- |
| Meaning    | Unknown/Missing | No characters       |
| Storage    | No value        | Zero-length value   |
| Comparison | Use `IS NULL`   | Use `= ''`          |

---

## 30. Difference between `COUNT(*)`, `COUNT(column)`, and `COUNT(DISTINCT column)`

| Feature            | COUNT(*)   | COUNT(column)   | COUNT(DISTINCT column) |
| ------------------ | ---------- | --------------- | ---------------------- |
| Counts all rows    | ✅ Yes      | ❌ No            | ❌ No                   |
| Ignores NULL       | ❌ No       | ✅ Yes           | ✅ Yes                  |
| Removes duplicates | ❌ No       | ❌ No            | ✅ Yes                  |
| Common use         | Total rows | Non-NULL values | Unique values          |
