### Set 7: BigQuery, SQL, Migration Project
  1. Tell me about your project.
  2. Write a JSON query to extract elements from JSON data in BigQuery.
  3. Write an INSERT query to insert data into a JSON column.
  4. Explain the flow of your migration project.
  5. How do you load an ORC file into BigQuery?
  6. How do you improve query performance in BigQuery?
  7. Write a query using the UNNEST() function.
  8. Display employees who joined in the last month.
  9. Write the syntax for a PIVOT query.
  10. Write a query to find missing IDs in a table.
  11. Write any Stored Procedure.
  12. What is the difference between Teradata and BigQuery?
  13. Why would you use BigQuery instead of Dataflow?
  14. Explain any Apache Beam function you have used.
  15. What are the different types of SQL functions?
---
### Set 8: Advanced SQL and BigQuery
  1. Create a table with STRUCT, ARRAY, and JSON data types.
  2. Write a SELECT query on a STRUCT field.
  3. How do you identify and print missing sequence values in a table?
  4. Write a query to UNNEST an ARRAY.
  5. Inventory Scenario:
		* Before March 5, 2022 → Use LIFO (Last In, First Out)
		* From March 5, 2022 onward → Use FIFO (First In, First Out)
	Write the approach or query logic.
  6. What are the Window Functions you are aware of?
  7. Calculate total sales amount for each customer for January and February.
  8. Find the top three highest-paid employees in each department.
  9. Find employees who joined in the last 30 days.
  10. How do you optimize a SQL query?
  11. If a datatype inconsistency occurs in a source field, how would you identify and handle it?
  12. What is the difference between RANK() and DENSE_RANK()?
  13. What complex data types have you handled in BigQuery?
---
### Set 9: Apache Beam, BigQuery, PySpark
  1. Write a query to return only users who have three consecutive login dates.
		Sample Data:
                | user_id | login_date |
                | ------- | ---------- |
                | 1       | 26-01-2024 |
                | 1       | 25-01-2024 |
                | 1       | 23-01-2024 |
                | 2       | 23-01-2024 |
                | 2       | 26-01-2024 |
                | 3       | 24-01-2024 |
                | 3       | 25-01-2024 |
                | 4       | 24-01-2024 |
                | 4       | 22-01-2024 |
                | 4       | 23-01-2024 |
  2. What are the different functions used in Apache Beam? Explain one.
  3. Create a table with STRUCT fields.
  4. What are the different methods to parse JSON data in BigQuery?
  5. What are Triggers in BigQuery?
  6. What is a DataFrame in PySpark?
  7. Between BigQuery and Dataflow, which would you choose and why?
  8. What complex data types are supported in BigQuery?
  9. What are the latest enhancements or features introduced in BigQuery?
  10. Write the syntax of a MERGE statement.
  11. Explain QUALIFY, RANK(), and DENSE_RANK().
  12. How do you load data from GCS to BigQuery while handling bad records?
  13. Write a Python function to replace values without using the replace() function.
---
### Set 10: Data Engineering, Apache Beam, PySpark
  1. Between BigQuery and Dataflow, which would you choose for transformation and processing? Why?
  2. Explain CROSS JOIN with sample records and output.
  3. Create a table using STRUCT data types.
  4. Explain Parallel Processing in Apache Beam.
  5. Write a query to extract values from JSON data.
  6. What is a BigQuery Trigger?
  7. What is Indexing? Explain the syntax.
  8. Which Apache Beam functions have you used?
  9. Write an Apache Beam function to replace a value.
  10. What PySpark functions have you used in projects?
  11. What data types have you handled in BigQuery?
  12. What is a Candidate Key?
  13. What is a DataFrame?
  14. Between Cloud Composer and Apache Airflow, which would you choose and why?
---
### Set 11: Real-Time Scenario-Based Questions
  1. Can you explain your previous project and your exact role in it?
  2. Suppose there are 4 million CSV files stored in a GCS bucket and they need to be loaded into BigQuery. What process would you follow?
  3. How would you validate data from 4 million files before loading it into BigQuery?
  4. What types of validations do you perform before loading data into BigQuery?
  5. If the target BigQuery schema is already defined, how would you validate all incoming CSV files?
  6. Suppose 200 CSV files need to be loaded from GCS to BigQuery. Approximately how much time would it take?
  7. Rate your expertise in:
      * BigQuery (1–5)
      * Dataflow (1–5)
      * Python (1–5)
  8. If selected for the project, what percentage of effort and commitment would you dedicate?
  9. Are you willing to spend additional time during critical deadlines or production issues?
---
### Set 12: GCP Data Engineer Interview Questions (June 2026)
  1. If you receive 20–25 CSV/Text files daily from multiple markets into one or more GCS buckets, how would you design a scalable, cost-effective, and production-ready pipeline to load them into BigQuery?
  2. How would data mapping work for 50 different markets, and how would the system identify which file has arrived?
  3. Once data lands in GCS, which GCP service would you use to process it and why?
  4. Explain the complete orchestration flow from file arrival in GCS until the data reaches the final reporting layer.
  5. How would you handle late-arriving data in Cloud Composer?
  6. If Task 1 must run first, Tasks 2 and 3 should run in parallel, and Task 4 should run after both complete, how would you define the DAG dependency?
  7. What is an ExternalTaskSensor in Airflow?
  8. Write a Python program to count the occurrences of values in a list (log records).
