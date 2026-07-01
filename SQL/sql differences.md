```sql
1. DELETE vs TRUNCATE vs DROP
2. WHERE vs HAVING vs QUALIFY
3. DDL vs DML vs DCL vs TCL
4. SCD Type 1 vs Type 2 vs Type 3 vs Type 4 vs Type 5 vs Type 6
5. COMMIT vs ROLLBACK vs SAVEPOINT
6. UNION vs UNION ALL vs INTERSECT vs EXCEPT (MINUS in Oracle)
7. Subquery vs Correlated Subquery
8. ROW_NUMBER() vs RANK() vs DENSE_RANK()
9. COUNT(*) vs COUNT(1) vs COUNT(column) vs COUNT(DISTINCT column)
10. CHAR vs VARCHAR vs NVARCHAR
11. COMPOSITE KEY vs SURROGATE KEY vs NATURAL KEY
12. PRIMARY KEY vs UNIQUE KEY vs FOREIGN KEY
13. INNER JOIN vs LEFT JOIN vs RIGHT JOIN vs FULL OUTER JOIN vs CROSS JOIN vs SELF JOIN
14. TABLE vs VIEW vs MATERIALIZED VIEW
15. CTE vs Temporary Table vs Table Variable
16. Stored Procedure vs Function vs Trigger
17. Aggregate Functions vs Window Functions
18. GROUP BY vs PARTITION BY
19. ISNULL() vs COALESCE() vs NVL() vs IFNULL()
20. CAST() vs SAFE_CAST() vs PARSE()
21. EXISTS vs IN vs ANY vs ALL vs NOT EXISTS vs NOT IN
22.  22. TOP vs LIMIT vs LIMIT + OFFSET
23. UNIQUE vs CHECK vs DEFAULT
24. Normalization vs Denormalization
25. 1NF vs 2NF vs 3NF vs BCNF
26. OLTP vs OLAP
27. Data Warehouse vs Data Mart
28. Star Schema vs Snowflake Schema vs Galaxy Schema
29. Fact Table vs Dimension Table vs Bridge Table
30. Authentication vs Authorization
31. SQL vs PL/SQL vs T-SQL
32. Logical Delete vs Physical Delete vs Soft Delete
```
## 1. DELETE vs TRUNCATE vs DROP

| Feature                 | DELETE                              | TRUNCATE                              | DROP                                        |
| ----------------------- | ----------------------------------- | ------------------------------------- | ------------------------------------------- |
| Definition              | Removes selected rows from a table. | Removes all rows from a table.        | Removes the entire database object.         |
| Purpose                 | Delete specific or all records.     | Quickly empty a table.                | Permanently remove a table/database object. |
| Performance             | Slow (row-by-row logging).          | Fast (minimal logging).               | Fastest (removes object).                   |
| Example Syntax          | `DELETE FROM emp WHERE dept='HR';`  | `TRUNCATE TABLE emp;`                 | `DROP TABLE emp;`                           |
| Best Use Case           | Delete filtered data.               | Clear staging tables.                 | Remove unused tables.                       |
| WHERE Clause            | ✅ Supported                         | ❌ Not Supported                       | ❌ Not Supported                             |
| Rollback                | ✅ Yes (until COMMIT)                | DB dependent (Oracle: Yes, MySQL: No) | DB dependent (usually No after COMMIT)      |
| Table Structure         | Retained                            | Retained                              | Removed                                     |
| Identity/Auto Increment | Not Reset                           | Usually Reset                         | Removed with table                          |

---

## 2. WHERE vs HAVING vs QUALIFY

| Feature                  | WHERE                                  | HAVING                                                           | QUALIFY                                                                                        |
| ------------------------ | -------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Definition               | Filters rows before grouping.          | Filters groups after aggregation.                                | Filters rows after window functions.                                                           |
| Purpose                  | Reduce input rows.                     | Filter aggregated results.                                       | Filter window function results.                                                                |
| Performance              | Fastest (early filtering).             | Slower (after aggregation).                                      | After window computation.                                                                      |
| Example Syntax           | `SELECT * FROM emp WHERE salary>5000;` | `SELECT dept,COUNT(*) FROM emp GROUP BY dept HAVING COUNT(*)>5;` | `SELECT *,ROW_NUMBER() OVER(PARTITION BY dept ORDER BY salary DESC) rn FROM emp QUALIFY rn=1;` |
| Best Use Case            | Normal filtering.                      | Aggregate filtering.                                             | Top-N per group.                                                                               |
| Uses Aggregate Functions | ❌                                      | ✅                                                                | ❌                                                                                              |
| Uses Window Functions    | ❌                                      | ❌                                                                | ✅                                                                                              |
| Execution Order          | Before GROUP BY                        | After GROUP BY                                                   | After WINDOW functions                                                                         |

---

## 3. DDL vs DML vs DCL vs TCL

| Feature         | DDL                           | DML                            | DCL                            | TCL                         |
| --------------- | ----------------------------- | ------------------------------ | ------------------------------ | --------------------------- |
| Definition      | Defines database objects.     | Manipulates table data.        | Controls permissions.          | Controls transactions.      |
| Purpose         | Create/modify schema.         | Insert/update/delete data.     | Grant/revoke access.           | Commit/rollback changes.    |
| Performance     | Metadata operation.           | Data operation.                | Security operation.            | Transaction operation.      |
| Example Syntax  | `CREATE TABLE emp(...);`      | `INSERT INTO emp VALUES(...);` | `GRANT SELECT ON emp TO user;` | `COMMIT;`                   |
| Best Use Case   | Schema management.            | Data changes.                  | User authorization.            | Transaction management.     |
| Common Commands | CREATE, ALTER, DROP, TRUNCATE | INSERT, UPDATE, DELETE, MERGE  | GRANT, REVOKE                  | COMMIT, ROLLBACK, SAVEPOINT |
| Affects Data    | Structure                     | Data                           | Permissions                    | Transactions                |

---

## 4. SCD Type 1 vs Type 2 vs Type 3 vs Type 4 vs Type 5 vs Type 6

| Feature           | Type 1               | Type 2                                 | Type 3                                | Type 4                            | Type 5                               | Type 6                        |
| ----------------- | -------------------- | -------------------------------------- | ------------------------------------- | --------------------------------- | ------------------------------------ | ----------------------------- |
| Definition        | Overwrite old value. | Keep full history using new rows.      | Store previous value in extra column. | History stored in separate table. | Type 4 + current value in dimension. | Combination of Type 1,2,3.    |
| Purpose           | Latest value only.   | Full historical tracking.              | Limited history.                      | Separate current/history.         | Fast reporting + history.            | Flexible historical analysis. |
| Performance       | Fastest              | Slower (more rows).                    | Moderate                              | Moderate                          | Moderate                             | Slowest                       |
| Example           | Update city.         | Insert new row with new surrogate key. | Add `previous_city`.                  | Current & history tables.         | Current table + history table.       | Mix of overwrite and history. |
| Best Use Case     | Correct mistakes.    | Regulatory/audit systems.              | Previous value comparison.            | Large historical datasets.        | BI reporting.                        | Enterprise DW.                |
| History Preserved | ❌                    | ✅ Full                                 | ✅ One Previous                        | ✅ Full                            | ✅ Full                               | ✅ Full                        |
| Extra Storage     | Low                  | High                                   | Medium                                | High                              | High                                 | Highest                       |

---

## 5. COMMIT vs ROLLBACK vs SAVEPOINT

| Feature               | COMMIT                         | ROLLBACK                    | SAVEPOINT                                  |
| --------------------- | ------------------------------ | --------------------------- | ------------------------------------------ |
| Definition            | Permanently saves transaction. | Undoes transaction changes. | Creates a checkpoint inside a transaction. |
| Purpose               | Make changes permanent.        | Undo changes.               | Partial rollback.                          |
| Performance           | Ends transaction.              | Reverses changes.           | Lightweight marker.                        |
| Example Syntax        | `COMMIT;`                      | `ROLLBACK;`                 | `SAVEPOINT sp1;`                           |
| Best Use Case         | After successful transaction.  | Error recovery.             | Complex transactions.                      |
| Undo Possible         | ❌                              | ✅                           | ✅ (to savepoint)                           |
| Transaction Continues | ❌ Ends                         | ❌ Ends                      | ✅ Continues                                |

---

## 6. UNION vs UNION ALL vs INTERSECT vs EXCEPT (MINUS)

| Feature                 | UNION                                      | UNION ALL                                      | INTERSECT                                      | EXCEPT / MINUS                              |
| ----------------------- | ------------------------------------------ | ---------------------------------------------- | ---------------------------------------------- | ------------------------------------------- |
| Definition              | Combines unique rows.                      | Combines all rows.                             | Returns common rows.                           | Returns rows only in first query.           |
| Purpose                 | Merge unique results.                      | Merge all results.                             | Find common records.                           | Find missing records.                       |
| Performance             | Slower (deduplication).                    | Fastest.                                       | Moderate.                                      | Moderate.                                   |
| Example Syntax          | `SELECT id FROM A UNION SELECT id FROM B;` | `SELECT id FROM A UNION ALL SELECT id FROM B;` | `SELECT id FROM A INTERSECT SELECT id FROM B;` | `SELECT id FROM A EXCEPT SELECT id FROM B;` |
| Best Use Case           | Remove duplicates.                         | Preserve duplicates.                           | Matching data.                                 | Data comparison.                            |
| Removes Duplicates      | ✅                                          | ❌                                              | ✅                                              | ✅                                           |
| Duplicate Rows Returned | No                                         | Yes                                            | No                                             | No                                          |

---

## 7. Subquery vs Correlated Subquery

| Feature                | Subquery                                                    | Correlated Subquery                                                                 |
| ---------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Definition             | Executes independently.                                     | Executes once for every outer row.                                                  |
| Purpose                | Provide intermediate result.                                | Compare each row with outer query.                                                  |
| Performance            | Faster.                                                     | Slower.                                                                             |
| Example Syntax         | `SELECT * FROM emp WHERE dept_id IN (SELECT id FROM dept);` | `SELECT * FROM emp e WHERE salary>(SELECT AVG(salary) FROM emp WHERE dept=e.dept);` |
| Best Use Case          | Independent filtering.                                      | Row-by-row comparison.                                                              |
| Depends on Outer Query | ❌                                                           | ✅                                                                                   |
| Execution Count        | Once                                                        | Once per outer row                                                                  |

---

## 8. ROW_NUMBER() vs RANK() vs DENSE_RANK()

| Feature          | ROW_NUMBER()                              | RANK()                              | DENSE_RANK()                              |
| ---------------- | ----------------------------------------- | ----------------------------------- | ----------------------------------------- |
| Definition       | Gives unique sequential numbers.          | Gives same rank with gaps.          | Gives same rank without gaps.             |
| Purpose          | Unique ordering.                          | Competition ranking.                | Dense ranking.                            |
| Performance      | Similar                                   | Similar                             | Similar                                   |
| Example Syntax   | `ROW_NUMBER() OVER(ORDER BY salary DESC)` | `RANK() OVER(ORDER BY salary DESC)` | `DENSE_RANK() OVER(ORDER BY salary DESC)` |
| Best Use Case    | Remove duplicates, Top-N.                 | Leaderboards.                       | Continuous ranking.                       |
| Duplicate Values | Different numbers                         | Same rank                           | Same rank                                 |
| Rank Gaps        | No                                        | Yes                                 | No                                        |

---

## 9. COUNT(*) vs COUNT(1) vs COUNT(column) vs COUNT(DISTINCT column)

| Feature        | COUNT(*)                        | COUNT(1)                         | COUNT(column)               | COUNT(DISTINCT column)                      |
| -------------- | ------------------------------- | -------------------------------- | --------------------------- | ------------------------------------------- |
| Definition     | Counts all rows.                | Counts all rows.                 | Counts non-NULL values.     | Counts unique non-NULL values.              |
| Purpose        | Total row count.                | Total row count.                 | Non-NULL count.             | Unique value count.                         |
| Performance    | Same as COUNT(1) in modern DBs. | Same as COUNT(*).                | Depends on NULLs.           | Slowest (deduplication).                    |
| Example Syntax | `COUNT(*)`                      | `COUNT(1)`                       | `COUNT(salary)`             | `COUNT(DISTINCT dept)`                      |
| Best Use Case  | Total records.                  | Total records.                   | Filled values.              | Unique counts.                              |
| Counts NULLs   | ✅ Rows with NULLs included      | ✅ Rows with NULLs included       | ❌ NULLs ignored             | ❌ NULLs ignored                             |
| Interview Tip  | Preferred standard              | Myth: not faster than `COUNT(*)` | Useful for nullable columns | Uses sorting/hash internally for uniqueness |


## 10. CHAR vs VARCHAR vs NVARCHAR

| Feature         | CHAR                                   | VARCHAR                             | NVARCHAR                                  |
| --------------- | -------------------------------------- | ----------------------------------- | ----------------------------------------- |
| Definition      | Fixed-length character string.         | Variable-length character string.   | Variable-length Unicode character string. |
| Purpose         | Store fixed-size text.                 | Store variable-size text.           | Store multilingual text.                  |
| Performance     | Slightly faster for fixed-length data. | Efficient storage for varying text. | Slightly slower due to Unicode.           |
| Example Syntax  | `CHAR(10)`                             | `VARCHAR(100)`                      | `NVARCHAR(100)`                           |
| Best Use Case   | Country codes, Gender.                 | Names, Emails.                      | International names, multilingual data.   |
| Storage         | Always reserves full length.           | Stores only actual characters.      | Stores actual Unicode characters.         |
| Unicode Support | ❌                                      | ❌                                   | ✅                                         |
| Trailing Spaces | Padded automatically.                  | No padding.                         | No padding.                               |

---

## 11. COMPOSITE KEY vs SURROGATE KEY vs NATURAL KEY

| Feature            | Composite Key                            | Surrogate Key                     | Natural Key                           |
| ------------------ | ---------------------------------------- | --------------------------------- | ------------------------------------- |
| Definition         | Combination of multiple columns.         | System-generated unique key.      | Business-meaningful column(s).        |
| Purpose            | Ensure uniqueness using multiple fields. | Provide stable unique identifier. | Identify records using business data. |
| Performance        | Moderate.                                | Best (single integer).            | Depends on data type.                 |
| Example Syntax     | `PRIMARY KEY(emp_id,dept_id)`            | `id INT IDENTITY`                 | `email VARCHAR UNIQUE`                |
| Best Use Case      | Many-to-many tables.                     | Data warehouses, dimensions.      | Business identifiers.                 |
| Business Meaning   | ✅                                        | ❌                                 | ✅                                     |
| Can Change         | Sometimes                                | Rarely                            | Often                                 |
| Recommended for DW | ❌                                        | ✅                                 | ❌                                     |

---

## 12. PRIMARY KEY vs UNIQUE KEY vs FOREIGN KEY

| Feature          | PRIMARY KEY                   | UNIQUE KEY                | FOREIGN KEY                                |
| ---------------- | ----------------------------- | ------------------------- | ------------------------------------------ |
| Definition       | Uniquely identifies each row. | Ensures unique values.    | References another table's key.            |
| Purpose          | Entity identification.        | Prevent duplicate values. | Maintain referential integrity.            |
| Performance      | Indexed.                      | Indexed.                  | Indexed in many DBs.                       |
| Example Syntax   | `PRIMARY KEY(id)`             | `UNIQUE(email)`           | `FOREIGN KEY(dept_id) REFERENCES dept(id)` |
| Best Use Case    | Main identifier.              | Alternate unique columns. | Table relationships.                       |
| NULL Allowed     | ❌                             | ✅ (DB dependent)          | ✅                                          |
| Duplicate Values | ❌                             | ❌                         | ✅                                          |
| Number per Table | One                           | Multiple                  | Multiple                                   |

---

## 13. INNER  vs LEFT JOIN vs RIGHT JOIN vs FULL OUTER JOIN vs CROSS JOIN vs SELF JOIN

| Feature        | INNER JOIN          | LEFT JOIN                  | RIGHT JOIN                 | FULL OUTER JOIN            | CROSS JOIN             | SELF JOIN                   |
| -------------- | ------------------- | -------------------------- | -------------------------- | -------------------------- | ---------------------- | --------------------------- |
| Definition     | Matching rows only. | All left + matching right. | All right + matching left. | All rows from both tables. | Cartesian product.     | Table joined with itself.   |
| Purpose        | Find common data.   | Preserve left table.       | Preserve right table.      | Compare complete datasets. | Generate combinations. | Hierarchical relationships. |
| Performance    | Fast                | Fast                       | Fast                       | Slower                     | Slowest                | Depends on data size.       |
| Example Syntax | `A INNER JOIN B`    | `A LEFT JOIN B`            | `A RIGHT JOIN B`           | `A FULL OUTER JOIN B`      | `A CROSS JOIN B`       | `emp e1 JOIN emp e2`        |
| Best Use Case  | Matching records.   | Missing data analysis.     | Preserve right table.      | Data reconciliation.       | Matrix generation.     | Employee-manager.           |
| Unmatched Rows | ❌                   | Left only                  | Right only                 | Both tables                | All combinations       | Depends on condition        |

---

## 14. TABLE vs VIEW vs MATERIALIZED VIEW

| Feature               | TABLE                    | VIEW                             | MATERIALIZED VIEW                          |
| --------------------- | ------------------------ | -------------------------------- | ------------------------------------------ |
| Definition            | Stores physical data.    | Virtual table from query.        | Stores query result physically.            |
| Purpose               | Permanent storage.       | Simplify queries/security.       | Faster reporting.                          |
| Performance           | Normal.                  | Executes base query every time.  | Fast reads.                                |
| Example Syntax        | `CREATE TABLE emp(...);` | `CREATE VIEW v_emp AS SELECT...` | `CREATE MATERIALIZED VIEW mv AS SELECT...` |
| Best Use Case         | Transactional storage.   | Reusable logic.                  | Analytics dashboards.                      |
| Stores Data           | ✅                        | ❌                                | ✅                                          |
| Automatically Updated | DML updates data.        | Always reflects latest data.     | Requires refresh (DB dependent).           |
| Storage Required      | High                     | None                             | High                                       |

---

## 15. CTE vs Temporary Table vs Table Variable

| Feature        | CTE                              | Temporary Table             | Table Variable                   |
| -------------- | -------------------------------- | --------------------------- | -------------------------------- |
| Definition     | Temporary result set in a query. | Temporary physical table.   | Temporary variable storing rows. |
| Purpose        | Improve query readability.       | Store intermediate results. | Small temporary datasets.        |
| Performance    | Good for single use.             | Best for large datasets.    | Best for small datasets.         |
| Example Syntax | `WITH cte AS (...)`              | `CREATE TEMP TABLE t AS...` | `DECLARE @t TABLE(...)`          |
| Best Use Case  | Recursive queries.               | Multi-step ETL.             | Small procedures.                |
| Scope          | Single query.                    | Session/transaction.        | Procedure/Batch.                 |
| Index Support  | ❌                                | ✅                           | Limited                          |

---

## 16. Stored Procedure vs Function vs Trigger

| Feature           | Stored Procedure        | Function               | Trigger                           |
| ----------------- | ----------------------- | ---------------------- | --------------------------------- |
| Definition        | Executable SQL program. | Returns a value/table. | Executes automatically on events. |
| Purpose           | Business logic.         | Calculations.          | Audit/validation.                 |
| Performance       | Good                    | Good                   | Automatic overhead.               |
| Example Syntax    | `CREATE PROCEDURE...`   | `CREATE FUNCTION...`   | `CREATE TRIGGER...`               |
| Best Use Case     | ETL, batch jobs.        | Reusable calculations. | Logging, auditing.                |
| Returns Value     | Optional                | Mandatory              | ❌                                 |
| Called Explicitly | ✅                       | ✅                      | ❌                                 |
| Triggered By      | User call               | SQL call               | INSERT/UPDATE/DELETE              |

---

## 17. Aggregate Functions vs Window Functions

| Feature                 | Aggregate Functions          | Window Functions                      |
| ----------------------- | ---------------------------- | ------------------------------------- |
| Definition              | Return one result per group. | Return result for each row.           |
| Purpose                 | Summarize data.              | Perform row-level analytics.          |
| Performance             | Faster.                      | Slightly slower.                      |
| Example Syntax          | `SUM(salary)`                | `SUM(salary) OVER(PARTITION BY dept)` |
| Best Use Case           | Reports.                     | Ranking, running totals.              |
| GROUP BY Required       | Usually                      | ❌                                     |
| Original Rows Preserved | ❌                            | ✅                                     |
| Common Functions        | SUM, AVG, MAX                | ROW_NUMBER, RANK, LAG, LEAD           |

---

## 18. GROUP BY vs PARTITION BY

| Feature                  | GROUP BY                         | PARTITION BY                       |
| ------------------------ | -------------------------------- | ---------------------------------- |
| Definition               | Groups rows into one output row. | Divides rows for window functions. |
| Purpose                  | Aggregate data.                  | Perform row-wise analytics.        |
| Performance              | Faster.                          | Slightly slower.                   |
| Example Syntax           | `GROUP BY dept`                  | `OVER(PARTITION BY dept)`          |
| Best Use Case            | Summary reports.                 | Running totals, ranking.           |
| Output Rows              | One per group.                   | Original rows retained.            |
| Used With                | Aggregate functions.             | Window functions.                  |
| Window Function Required | ❌                                | ✅                                  |

---

## 19. ISNULL() vs COALESCE() vs NVL() vs IFNULL()

| Feature             | ISNULL()                      | COALESCE()                    | IFNULL()                |
| ------------------- | ----------------------------- | ----------------------------- | ----------------------- |
| Definition          | Replaces NULL with a value.   | Returns first non-NULL value. | MySQL NULL replacement. |
| Purpose             | Handle NULLs.                 | Handle multiple NULL options. | Handle NULLs in MySQL.  |
| Performance         | Slightly faster (SQL Server). | ANSI Standard.                | MySQL specific.         |
| Example Syntax      | `ISNULL(salary,0)`            | `COALESCE(col1,col2,0)`       | `IFNULL(salary,0)`      |
| Best Use Case       | SQL Server.                   | Cross-platform SQL.           | MySQL.                  |
| Number of Arguments | 2                             | Multiple                      | 2                       |
| ANSI Standard       | ❌                           | ✅                            | ❌                      |
| Database Support    | SQL Server                    | Most databases                | MySQL                   |



## 20. CAST() vs SAFE_CAST() vs PARSE()

| Feature               | CAST()                             | SAFE_CAST()                                    | PARSE()                                              |
| --------------------- | ---------------------------------- | ---------------------------------------------- | ---------------------------------------------------- |
| Definition            | Converts one data type to another. | Converts data safely; returns NULL on failure. | Converts formatted strings into specific data types. |
| Purpose               | Standard type conversion.          | Avoid conversion errors.                       | Parse formatted text.                                |
| Performance           | Fast                               | Slight overhead                                | Similar to CAST()                                    |
| Example Syntax        | `CAST(age AS INT)`                 | `SAFE_CAST(age AS INT)`                        | `PARSE_DATE('%Y-%m-%d','2026-01-01')`                |
| Best Use Case         | Clean data.                        | Dirty or uncertain data.                       | Date, Time, Timestamp parsing.                       |
| Error on Invalid Data | ✅                                  | ❌ (Returns NULL)                               | ✅                                                    |
| Common In             | All DBs                            | BigQuery                                       | BigQuery                                             |

---

## 21. EXISTS vs IN vs ANY vs ALL vs NOT EXISTS vs NOT IN

| Feature        | EXISTS                     | IN                      | ANY                     | ALL                          | NOT EXISTS              | NOT IN                    |
| -------------- | -------------------------- | ----------------------- | ----------------------- | ---------------------------- | ----------------------- | ------------------------- |
| Definition     | Checks if rows exist.      | Checks value in a list. | Compare with any value. | Compare with all values.     | Checks absence of rows. | Checks value not in list. |
| Purpose        | Existence check.           | Membership check.       | Flexible comparison.    | Compare against every value. | Anti-join logic.        | Exclude values.           |
| Performance    | Best for large subqueries. | Good for small lists.   | Moderate.               | Moderate.                    | Efficient anti-join.    | Can be slow with NULLs.   |
| Example Syntax | `WHERE EXISTS(...)`        | `WHERE id IN (...)`     | `salary > ANY(...)`     | `salary > ALL(...)`          | `WHERE NOT EXISTS(...)` | `WHERE id NOT IN(...)`    |
| Best Use Case  | Correlated subqueries.     | Static lists.           | Range comparison.       | Highest/Lowest comparisons.  | Missing records.        | Small non-NULL lists.     |
| NULL Handling  | Safe                       | Safe                    | Safe                    | Safe                         | Safe                    | NULL may return no rows   |

---

## 22. TOP vs LIMIT vs LIMIT + OFFSET

| Feature             | TOP                   | LIMIT                        | LIMIT + OFFSET                                                              |
| ------------------- | --------------------- | ---------------------------- | --------------------------------------------------------------------------- |
| Definition          | Returns first N rows. | Limits result rows.          | Skips N rows, then returns the next set of rows.                            |
| Purpose             | Row limiting.         | Row limiting.                | Implement pagination.                                                       |
| Performance         | Similar               | Similar                      | Large OFFSET values can be slower because skipped rows are still processed. |
| Example Syntax      | `TOP 10`              | `LIMIT 10`                   | `SELECT * FROM employees LIMIT 10 OFFSET 20;`                               |
| Best Use Case       | SQL Server.           | MySQL, PostgreSQL, BigQuery. | Pagination in applications.                                                 |
| Supports Pagination | Limited               | With OFFSET                   | ✅                                                                           |
| Database            | SQL Server            | MySQL/Postgres/BigQuery       | ✅                                                                           |

---

## 23. UNIQUE vs CHECK vs DEFAULT

| Feature               | UNIQUE                     | CHECK                             | DEFAULT                    |
| --------------------- | -------------------------- | --------------------------------- | -------------------------- |
| Definition            | Prevents duplicate values. | Validates values using condition. | Assigns default value.     |
| Purpose               | Ensure uniqueness.         | Enforce business rules.           | Auto-fill missing values.  |
| Performance           | Indexed.                   | Validation overhead.              | Negligible.                |
| Example Syntax        | `UNIQUE(email)`            | `CHECK(age>=18)`                  | `DEFAULT CURRENT_DATE`     |
| Best Use Case         | Emails, IDs.               | Data validation.                  | Default timestamps/status. |
| Allows NULL           | Usually Yes                | Yes                               | Yes                        |
| Prevents Invalid Data | Duplicate only             | ✅                                 | ❌                          |

---

## 24. Normalization vs Denormalization

| Feature         | Normalization                     | Denormalization                      |
| --------------- | --------------------------------- | ------------------------------------ |
| Definition      | Splits data into multiple tables. | Combines data into fewer tables.     |
| Purpose         | Reduce redundancy.                | Improve read performance.            |
| Performance     | Faster writes.                    | Faster reads.                        |
| Example         | Customer & Orders separate.       | Customer details repeated in Orders. |
| Best Use Case   | OLTP systems.                     | OLAP/Data Warehouse.                 |
| Data Redundancy | Low                               | High                                 |
| Storage         | Less                              | More                                 |
| Joins Required  | More                              | Fewer                                |

---

## 25. 1NF vs 2NF vs 3NF vs BCNF

| Feature       | 1NF                        | 2NF                        | 3NF                           | BCNF                                  |
| ------------- | -------------------------- | -------------------------- | ----------------------------- | ------------------------------------- |
| Definition    | Atomic values only.        | Remove partial dependency. | Remove transitive dependency. | Every determinant is a candidate key. |
| Purpose       | Basic normalization.       | Eliminate redundancy.      | Improve integrity.            | Strongest normalization.              |
| Example       | No comma-separated values. | Separate product details.  | Separate department table.    | Resolve candidate key anomalies.      |
| Best Use Case | Initial design.            | Composite keys.            | Most OLTP systems.            | Advanced database design.             |
| Redundancy    | High                       | Lower                      | Low                           | Lowest                                |
| Complexity    | Low                        | Medium                     | High                          | Highest                               |

---

## 26. OLTP vs OLAP

| Feature       | OLTP                           | OLAP                             |
| ------------- | ------------------------------ | -------------------------------- |
| Definition    | Transaction processing system. | Analytical processing system.    |
| Purpose       | Run business operations.       | Perform reporting and analytics. |
| Performance   | Fast inserts/updates.          | Fast complex queries.            |
| Example       | Banking, E-commerce.           | Data Warehouse, BI.              |
| Best Use Case | Daily transactions.            | Business intelligence.           |
| Data Volume   | Current data.                  | Historical data.                 |
| Query Type    | Short/simple.                  | Long/complex.                    |
| Normalization | Highly normalized.             | Denormalized.                    |

---

## 27. Data Warehouse vs Data Mart

| Feature       | Data Warehouse                | Data Mart                        |
| ------------- | ----------------------------- | -------------------------------- |
| Definition    | Enterprise-wide repository.   | Department-specific repository.  |
| Purpose       | Organization analytics.       | Team analytics.                  |
| Performance   | Handles enterprise workloads. | Faster for departmental queries. |
| Example       | Company-wide sales data.      | Finance sales mart.              |
| Best Use Case | Enterprise BI.                | Business units.                  |
| Scope         | Entire organization.          | Single department.               |
| Size          | Large                         | Smaller                          |

---

## 28. Star Schema vs Snowflake Schema vs Galaxy Schema

| Feature       | Star Schema                            | Snowflake Schema                        | Galaxy Schema                            |
| ------------- | -------------------------------------- | --------------------------------------- | ---------------------------------------- |
| Definition    | One fact with denormalized dimensions. | Normalized dimensions.                  | Multiple fact tables sharing dimensions. |
| Purpose       | Fast querying.                         | Reduce redundancy.                      | Enterprise analytics.                    |
| Performance   | Fastest.                               | Slightly slower.                        | Moderate.                                |
| Example       | Sales Fact + Customer Dim.             | Customer normalized into Address table. | Sales & Inventory facts.                 |
| Best Use Case | BI dashboards.                         | Large dimensions.                       | Enterprise DW.                           |
| Joins         | Few                                    | More                                    | Many                                     |
| Storage       | High                                   | Low                                     | Medium                                   |

---

## 29. Fact Table vs Dimension Table vs Bridge Table

| Feature               | Fact Table                 | Dimension Table                | Bridge Table                         |
| --------------------- | -------------------------- | ------------------------------ | ------------------------------------ |
| Definition            | Stores measurable metrics. | Stores descriptive attributes. | Resolves many-to-many relationships. |
| Purpose               | Business measurements.     | Context information.           | Connect dimensions/facts.            |
| Performance           | Large scans.               | Fast lookups.                  | Additional join.                     |
| Example               | Sales amount.              | Customer details.              | Student-Course mapping.              |
| Best Use Case         | KPIs.                      | Filtering/reporting.           | Many-to-many modeling.               |
| Contains Measures     | ✅                          | ❌                              | ❌                                    |
| Contains Foreign Keys | ✅                          | ❌                              | ✅                                    |

---

## 30. Authentication vs Authorization

| Feature        | Authentication       | Authorization           |
| -------------- | -------------------- | ----------------------- |
| Definition     | Verifies identity.   | Verifies permissions.   |
| Purpose        | Login validation.    | Access control.         |
| Performance    | Login-time check.    | Resource access check.  |
| Example        | Username & Password. | IAM Role, GRANT SELECT. |
| Best Use Case  | User verification.   | Permission management.  |
| Question Asked | "Who are you?"       | "What can you access?"  |
| Happens First  | ✅                    | ❌                       |

---

## 31. SQL vs PL/SQL vs T-SQL

| Feature            | SQL                      | PL/SQL                       | T-SQL                            |
| ------------------ | ------------------------ | ---------------------------- | -------------------------------- |
| Definition         | Standard query language. | Oracle procedural SQL.       | SQL Server procedural SQL.       |
| Purpose            | Query data.              | Business logic.              | Business logic.                  |
| Performance        | Query execution.         | Stored programs.             | Stored programs.                 |
| Example Syntax     | `SELECT * FROM emp;`     | `BEGIN...END;`               | `BEGIN...END`                    |
| Best Use Case      | CRUD operations.         | Oracle procedures/functions. | SQL Server procedures/functions. |
| Supports Variables | ❌                        | ✅                            | ✅                                |
| Loops & Conditions | ❌                        | ✅                            | ✅                                |
| Database           | ANSI                     | Oracle                       | SQL Server                       |

---

## 32. Logical Delete vs Physical Delete vs Soft Delete

| Feature              | Logical Delete             | Physical Delete              | Soft Delete                         |
| -------------------- | -------------------------- | ---------------------------- | ----------------------------------- |
| Definition           | Marks record as deleted.   | Permanently removes record.  | Uses a flag/status to hide records. |
| Purpose              | Preserve history.          | Free storage.                | Easy recovery.                      |
| Performance          | Slight filtering overhead. | Fast storage cleanup.        | Similar to logical delete.          |
| Example Syntax       | `UPDATE emp SET active=0`  | `DELETE FROM emp WHERE id=1` | `UPDATE emp SET is_deleted=TRUE`    |
| Best Use Case        | Audit systems.             | Temporary/staging data.      | Applications requiring recovery.    |
| Data Recoverable     | ✅                          | ❌                            | ✅                                   |
| Storage Saved        | ❌                          | ✅                            | ❌                                   |
| Common in Production | ✅                          | Limited                      | ✅                                   |


