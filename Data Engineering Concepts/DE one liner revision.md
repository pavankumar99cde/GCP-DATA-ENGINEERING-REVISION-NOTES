
| Terminology                              | Simple Definition                                                                               |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Data Warehouse**                       | A centralized database that stores data from multiple sources for reporting and analytics.   ( **Snowflake**, **Google BigQuery**, **Amazon Redshift**, **Azure Synapse Analytics**)        |
| **Data Mart**                            | A smaller version of a data warehouse designed for a specific department like Sales or Finance. |
| **Data Lake**                            | A storage system that holds raw structured, semi-structured, and unstructured data.          (**Amazon S3**, **Azure Data Lake Storage (ADLS)**, **Google Cloud Storage (GCS)**)            |
| **Data Lakehouse**                       | Combines the flexibility of a data lake with the management features of a data warehouse.       |
| **ETL (Extract, Transform, Load)**       | Extract data from sources, transform it, then load it into the destination.                     |
| **ELT (Extract, Load, Transform)**       | Extract data, load it first into storage, then transform it inside the database.                |
| **Data Pipeline**                        | An automated process that moves data from one system to another.                                |
| **Data Ingestion**                       | The process of collecting data from various sources into a storage system.                      |
| **Batch Processing**                     | Processing large amounts of data at scheduled intervals.                                        |
| **Stream Processing**                    | Processing data continuously as it arrives in real time.                                        |
| **Data Transformation**                  | Converting data into the required format for analysis.                                          |
| **Data Cleansing**                       | Removing duplicates, correcting errors, and handling missing values.                            |
| **Data Validation**                      | Ensuring data meets predefined quality rules.                                                   |
| **Data Quality**                         | Measuring data based on accuracy, completeness, consistency, and reliability.                   |
| **Data Modeling**                        | Designing how data is organized and related in a database.                                      |
| **Schema**                               | The structure of a database, including tables, columns, and relationships.                      |
| **Schema-on-Write**                      | Data is validated before storing it (common in data warehouses).                                |
| **Schema-on-Read**                       | Data is stored first and interpreted when read (common in data lakes).                          |
| **Fact Table**                           | Stores measurable business data like sales, revenue, or orders.                                 |
| **Dimension Table**                      | Stores descriptive information like customer, product, or date details.                         |
| **Star Schema**                          | One fact table connected directly to multiple dimension tables.                                 |
| **Snowflake Schema**                     | A normalized version of the star schema where dimensions are split into multiple tables.        |
| **Primary Key**                          | A unique identifier for each record in a table.                                                 |
| **Foreign Key**                          | A column that links one table to another.                                                       |
| **Surrogate Key**                        | A system-generated unique key used instead of business keys.                                    |
| **Business Key**                         | A real-world identifier such as Employee ID or Customer ID.                                     |
| **Normalization**                        | Organizing data to reduce redundancy.                                                           |
| **Denormalization**                      | Combining tables to improve query performance.                                                  |
| **Partitioning**                         | Dividing large tables into smaller parts for faster queries.                                    |
| **Bucketing**                            | Dividing data into fixed buckets based on a hash function.                                      |
| **Indexing**                             | Creating a structure that speeds up data retrieval.                                             |
| **Clustering**                           | Physically organizing related data together for efficient queries.                              |
| **Metadata**                             | Data that describes other data (table names, column types, etc.).                               |
| **Data Lineage**                         | Tracking where data comes from and how it changes.                                              |
| **Data Governance**                      | Policies and standards for managing data securely and consistently.                             |
| **Data Catalog**                         | A searchable inventory of available datasets.                                                   |
| **Data Security**                        | Protecting data from unauthorized access.                                                       |
| **Data Encryption**                      | Converting data into a secure format that only authorized users can read.                       |
| **Data Masking**                         | Hiding sensitive information while keeping the data usable.                                     |
| **CDC (Change Data Capture)**            | Capturing only new or modified records since the last load.                                     |
| **SCD (Slowly Changing Dimension)**      | Techniques for managing changes in dimension data over time.                                    |
| **OLTP (Online Transaction Processing)** | Optimized for fast inserts, updates, and deletes (transactional systems).                       |
| **OLAP (Online Analytical Processing)**  | Optimized for complex analytical queries and reporting.                                         |
| **Data Mesh**                            | A decentralized approach where domain teams own their data.                                     |
| **Data Fabric**                          | An architecture that connects and manages data across multiple environments.                    |
| **Data Orchestration**                   | Coordinating multiple data pipeline tasks and workflows.         (**Apache Airflow**, **Dagster**, **Prefect**     )                                        |
| **Workflow**                             | A sequence of tasks executed in a defined order.                                                |
| **Scheduler**                            | A tool that runs jobs at specified times or intervals.                                          |
| **Checkpointing**                        | Saving processing progress to recover from failures.                                            |
| **Idempotency**                          | Running the same job multiple times produces the same result.                                   |
| **Exactly Once Processing**              | Ensures each record is processed only once.                                                     |
| **At Least Once Processing**             | Records may be processed more than once.                                                        |
| **At Most Once Processing**              | Records are processed once or not at all.                                                       |
| **Data Replication**                     | Copying data from one location to another.                                                      |
| **Data Backup**                          | Creating copies of data for recovery.                                                           |
| **Disaster Recovery**                    | Restoring systems and data after failures.                                                      |
| **Data Compression**                     | Reducing storage space by compressing data.                                                     |
| **Data Serialization**                   | Converting data into a format suitable for storage or transmission (JSON, Avro, Protobuf).      |
| **Parquet**                              | A columnar file format optimized for analytics.                                                 |
| **ORC**                                  | A highly compressed columnar storage format for big data.                                       |
| **Avro**                                 | A row-based serialization format with schema support.                                           |
| **Delta Table**                          | A table format that supports ACID transactions on data lakes.                                   |
| **Iceberg Table**                        | An open table format for managing large analytical datasets.                                    |
| **Hudi Table**                           | A table format supporting incremental processing and updates.                                   |

