### Set 1: Airflow, BigQuery, SQL
  1. Can you please introduce yourself?
  2. What are Airflow Operators and what are their types?
  3. What is the difference between Partitioning and Clustering in BigQuery?
  4. How do you perform data validation before loading data?
  5. What is a Materialized View in BigQuery?
  6. What is an Authorized View and how do you provide access to it?
  7. What are the different types of SQL Joins? Explain each with an example.
  8. How do you schedule a DAG in Airflow, and what is a Cron Expression?
  9. How would you find duplicate records in a SQL table?
  10. How do you pass runtime variables in Airflow?
  11. What is the syntax of the BigQuery MERGE statement?
---
### Set 2: Dataflow, Apache Beam, BigQuery Streaming
  1. Self Introduction
  2. How would you design a pipeline for data arriving every minute?
  3. How do you insert data into BigQuery?
  4. How do you maintain data in BigQuery and deliver it to real-time streams?
  5. What are the windowing techniques in Apache Beam?
  6. How would you handle a high volume of incoming data within a one-minute period in BigQuery?
  7. How do you prevent duplicate records during data ingestion?
---
### Set 3: SQL, Airflow, Apache Beam
  1. Suppose people are seated in a row:
```python
people = [1, 2, 6, 1, 1, 9, 1, 3]
```
	If a person is seated at position 3, how many people can they see?
  2. What is TensorFlow?
  3. What is the difference between RANK(), DENSE_RANK(), and ROW_NUMBER()? When would you use each?
  4. If a table has both Partitioning and Clustering enabled, how does BigQuery process the data?
  5. What are the ShortCircuitOperator and BranchPythonOperator in Airflow?
  6. How can you pass values to a BashOperator without using XCom?
  7. Explain DAG Dependencies, Concurrency, and Parallelism in Airflow.
  8. What query optimization techniques do you use in daily projects?
  9. How do you read multiple files in Apache Beam? Provide a code example.
  10. Write a query to fill NULL salary values with the previous employee's salary.
  11. Define:
* PCollection  * PTransform   * Pipeline


 12. What are the key features of BigQuery?
 13. How would you determine whether weekends exist between two dates?
 14. What are the different types of functions in Apache Beam?
 15. Explain the Reshuffle transform in Apache Beam.
---
### Set 4: BigQuery, Airflow, Apache Beam
  1. Explain ROW_NUMBER(), RANK(), and DENSE_RANK().
  2. Explain BigQuery pricing and cost optimization techniques.
  3. How do you initiate an Apache Beam pipeline to read data from BigQuery?
  4. Write a pseudo DAG to:
* Run every hour.
* Run every minute using a cron expression.
 5. Write a sample Airflow DAG using:
* BashOperator
* PythonOperator
    to list files from a GCS bucket.
 6. How does Clustering improve query performance?
 7. Can you update a table's Partitioning configuration after the table has been created?
---
### Set 5: BigQuery, Migration Projects, SQL
  1. Tell me about your project.
  2. Write a BigQuery query to extract values from JSON data.
  3. Write an INSERT statement to load data into a JSON column.
  4. Explain the end-to-end flow of your migration project.
  5. How do you load an ORC file into BigQuery?
  6. How do you improve query performance in BigQuery?
  7. Write a query using the UNNEST() function.
  8. Display employees who joined in the last month using an Employee table.
  9. Write the syntax for a PIVOT query.
  10. Write a query to find missing IDs in a table.
  11. Write a sample Stored Procedure.
  12. What is the difference between Teradata and BigQuery?
  13. Why would you use BigQuery instead of Dataflow?
  14. Name and explain some commonly used Apache Beam functions.
  15. What are the different types of SQL functions?
---
### Set 6: Advanced Data Engineer Questions
  1. Explain BigQuery Partitioning Types.
  2. Explain BigQuery Clustering and its limitations.
  3. Difference between Batch Processing and Stream Processing.
  4. Explain Pub/Sub message flow in GCP.
  5. What is the difference between DataflowRunner and DirectRunner?
  6. What is Windowing and Triggering in Apache Beam?
  7. Explain Watermarks and Allowed Lateness.
  8. How does BigQuery Streaming Insert work?
  9. What is the Storage Write API?
  10. How do you implement SCD Type 1 and SCD Type 2 in BigQuery?
  11. Difference between Views and Materialized Views.
  12. What are Common Table Expressions (CTEs)?
  13. Explain QUALIFY in BigQuery.
  14. Difference between UNION and UNION ALL.
  15. Explain ARRAY and STRUCT data types in BigQuery.
  16. What is Data Skew and how do you handle it?
  17. Explain Idempotency in Data Pipelines.
  18. How do you monitor a Dataflow job?
  19. What are Side Inputs in Apache Beam?
  20. Explain Dead Letter Queue (DLQ) architecture.
