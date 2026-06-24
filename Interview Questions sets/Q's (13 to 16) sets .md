### Set 13: Dataflow, BigQuery, Python, SQL
  1. Self-Introduction
  2. Explain your project.
  3. What are your roles and responsibilities in the project?
  4. What are your day-to-day activities as a Data Engineer?
  5. Explain a real-time Dataflow architecture to process and load 1 TB of text file data.
  6. How do you handle late-arriving data in a Dataflow job?
  7. What is the difference between Dataflow and Dataproc?
  8. What is the difference between mutable and immutable data types in Python?
  9. Python Coding:
Given:
```python
nums = [2,7,11,15]
target = 9
```
Return:
```python
[0,1]
```
How would you solve this problem?
  10. Using a CTE, write a query to find the 3rd highest salary from an Employee table.
  11. Write an incremental load SQL query using an assumed source and target table.
  12. Write an Apache Beam function that you have used in your project.
  13. How do you validate data before inserting it into BigQuery?
  14. What methods are available for:
* Batch data ingestion?
* Streaming data ingestion?
Explain the flow.
  15. Write a SQL query to remove duplicate records from a table.
---
### Set 14: Airflow, GCS, Validation, DAG Design
  1. Self-Introduction
  2. Explain your project and responsibilities.
 ### Follow-up Questions:
  3. What was the design structure of your DAGs?
  4. How do you identify that a file has arrived in GCS?
  5. What validations did you perform?
  6. Explain the validation logic implemented in your previous project.
  7. Explain your project folder structure.
  8. Write an Airflow DAG using:
* PythonOperator
* BashOperator
  9. Explain each DAG parameter:
* dag_id
* schedule_interval
* start_date
* retries
* retry_delay
* catchup
* default_args
  10. How would you handle late-arriving data?
  11. How do you configure Airflow for parallel processing?
 ### DAG-Level Settings:
* max_active_runs
* concurrency
 ### Airflow-Level Settings:
* parallelism
* worker_concurrency
  12. Write Python code to read a file and execute it through an Airflow DAG.
  13. Write a query to identify duplicate records.
---
### Set 15: Python Coding Round
  1. What is the output of the following code?
```python
try:
    a = (1, 2, [3, 4], 5)
    a[2][0] = 10
except:
    print("Exception occurred")
print(a)
```
  2. Given:
```python
lst = [1, 2, 3, 4]
```
Write a single-line Python statement:
* Even numbers → square the value
* Odd numbers → subtract 1
Expected Output:
```python
[0, 4, 2, 16]
```
  3. Transaction and Product Tables
          Transaction Table:
          | product_id | user_id | purchased_date |
          | ---------- | ------- | -------------- |
          | 123        | US101   | 12-01-2024     |
          | 122        | US201   | 18-03-2024     |
          | 124        | US101   | 29-02-2024     |
          | 123        | US301   | 22-05-2024     |
          | 123        | US401   | 25-03-2024     |
          | 456        | US401   | 25-03-2024     |
          | 123        | US601   | 12-01-2024     |
          Product Table:
          | product_id | product_name | price |
          | ---------- | ------------ | ----- |
          | 123        | Earphone     | 50    |
          | 122        | Mouse        | 10    |
          | 124        | Keyboard     | 50    |
          Write Python (Pandas/Numpy) code to generate:
          | product_id | product_name | items_sold | total_revenue |
          | ---------- | ------------ | ---------- | ------------- |
          | 123        | Earphone     | 3          | 150           |
  4. Given a sequence with one missing value, write Python code to identify the missing number.
---
### Set 16: Materialized Views, Authorized Views, Dataflow
  1. Where is data physically stored for a Materialized View?
  2. What is the difference between:
       Materialized View vs Authorized View       
  3. How do you trigger a Dataflow job from Airflow?
  4. Write a sample Airflow DAG to trigger a Dataflow job.
  5. Explain your project architecture.
  6. Explain Dataflow architecture end-to-end.
  7. How do you monitor and troubleshoot a failed Dataflow job?
  8. How do you prevent duplicate records in a streaming Dataflow pipeline?
  9. What is the difference between Fixed Window, Sliding Window, and Session Window?
  10. Explain:
      * PCollection
      * PTransform
      * Pipeline
      * Windowing
      * Triggering
      * Watermark
---
