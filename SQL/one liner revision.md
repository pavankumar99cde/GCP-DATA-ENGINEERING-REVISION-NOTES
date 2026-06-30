
| Interview Question                                         | One-Line Answer                                                                                      |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Why is `EXISTS` often faster than `IN` for large datasets? |  `EXISTS` stops searching after the first match, while `IN` may evaluate the entire subquery. |
| Why is `UNION ALL` faster than `UNION`?                    |  `UNION ALL` skips duplicate elimination, avoiding an expensive sort or hash operation.       |
| Why can `SELECT *` hurt query performance?                 |  it reads unnecessary columns, increasing I/O, memory usage, and network transfer.            |
| Why are functions on indexed columns bad for performance?  |  they prevent index usage, forcing a full table scan.                                         |
| Why is `COUNT(*)` usually preferred over `COUNT(column)`?  |  `COUNT(*)` counts all rows, while `COUNT(column)` ignores NULL values.                       |
| Why are correlated subqueries slower than joins?           |  the subquery executes once for every outer row, increasing execution time.                   |
| Why should you filter data before joining tables?          |  reducing rows early minimizes the amount of data processed during joins.                     |
| Why can `DISTINCT` be expensive?                           |  SQL must sort or hash the data to remove duplicates.                                         |
| Why do window functions outperform self-joins?             |  they compute row-based calculations without repeatedly joining the same table.               |
| Why is `ROW_NUMBER()` preferred for Top-N queries?         |  it efficiently ranks rows without requiring multiple nested queries.                         |
| Why should you avoid unnecessary `ORDER BY`?               |  sorting large datasets consumes CPU, memory, and temporary storage.                          |
| Why are CTEs sometimes slower than subqueries?             |  some databases materialize CTEs instead of optimizing them inline.                           |
| Why can too many joins reduce performance?                 |  each join increases execution complexity and intermediate result sizes.                      |
| Why is partition pruning important?                        |  it scans only relevant partitions instead of the entire table.                               |
| Why is clustering beneficial after partitioning?           |  it organizes data within partitions, reducing the amount of data scanned.                    |
| Why should predicates be selective?                        |  highly selective filters reduce the number of rows processed.                                |
| Why do indexes slow down INSERT and UPDATE operations?     |  indexes must also be updated whenever the data changes.                                      |
| Why is `LEFT JOIN` sometimes slower than `INNER JOIN`?     |  it must preserve unmatched rows in addition to matched rows.                                 |
| Why should data types match in join conditions?            |  implicit type conversions can prevent index usage and slow joins.                            |
| Why are Cartesian joins dangerous?                         |  they produce every possible row combination, causing exponential data growth.                |
| Why can `OR` conditions reduce performance?                |  they often prevent efficient index usage and increase scans.                                 |
| Why is `CASE` preferred over multiple nested queries?      |  it performs conditional logic within a single query execution.                               |
| Why should you avoid repeated scalar subqueries?           |  they execute multiple times, increasing CPU utilization.                                     |
| Why are covering indexes faster?                           |  all required columns are available in the index without accessing the table.                 |
| Why is query execution plan analysis important?            |  it identifies bottlenecks like scans, expensive joins, and unnecessary sorts.                |
| Why should statistics be updated regularly?                |  the optimizer depends on accurate statistics to choose efficient execution plans.            |
| Why does data skew affect joins?                           |  uneven data distribution creates workload imbalance and slower execution.                    |
| Why can NULL values affect query results?                  |  NULL follows three-valued logic and behaves differently in comparisons.                      |
| Why is `NOT EXISTS` generally better than `NOT IN`?        |  `NOT IN` can produce unexpected results when NULL values exist.                              |
| Why is pagination with `OFFSET` expensive?                 |  the database still scans skipped rows before returning the requested ones.                   |
| Why is keyset pagination faster than `OFFSET`?             |  it directly starts from the last retrieved key instead of skipping rows.                     |
| Why should large tables be partitioned?                    |  partitioning reduces scan size and improves query performance.                               |
| Why are materialized views faster than normal views?       |  their results are precomputed and stored physically.                                         |
| Why can nested views hurt performance?                     |  they create complex execution plans that are harder to optimize.                             |
| Why should aggregations happen after filtering?            |  fewer rows need to be grouped, reducing computation time.                                    |
| Why is `HAVING` slower than `WHERE`?                       |  `HAVING` filters after aggregation, while `WHERE` filters before aggregation.                |
| Why should indexes be created only when necessary?         |  excessive indexes increase storage and slow write operations.                                |
| Why do execution plans change over time?                   |  data volume, statistics, indexes, and optimizer decisions evolve.                            |
| Why is normalization not always best for analytics?        |  highly normalized tables require many joins, reducing analytical query performance.          |
| Why are star schemas preferred in data warehouses?         |  fewer joins improve aggregation and reporting performance.                                   |

