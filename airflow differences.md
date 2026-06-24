# Quick Interview One-Liners

| Question                                       | Simple Answer                                             |
| ---------------------------------------------- | --------------------------------------------------------- |
| Poke vs Reschedule                             | Poke keeps worker busy, Reschedule releases worker.       |
| PythonOperator vs BashOperator vs TaskFlow API | Python code, Bash command, Modern decorator-based Python. |
| BranchPythonOperator vs ShortCircuitOperator   | Choose path vs Stop/Continue workflow.                    |
| Connections vs Variables vs Secrets Backend    | Connection details, Config values, Secure credentials.    |
| SLA vs Execution Timeout                       | Alert on delay vs Fail task on timeout.                   |
| Task Timeout vs DAG Timeout                    | Task limit vs Entire workflow limit.                      |
| TriggerDagRunOperator vs ExternalTaskSensor    | Trigger another DAG vs Wait for another DAG.              |
| TaskGroups vs SubDAGs                          | Lightweight grouping vs Deprecated nested DAG.            |
| Dynamic DAGs vs Dynamic Task Mapping           | Create DAGs dynamically vs Create tasks dynamically.      |
| Airflow Batch vs Dataflow Streaming            | Scheduled processing vs Real-time processing.             |
| Airflow vs Cloud Composer                      | Self-managed vs Google-managed Airflow.                   |


## 1. Scheduler vs Executor vs Worker

| Feature        | Scheduler                                | Executor                      | Worker                 |
| -------------- | ---------------------------------------- | ----------------------------- | ---------------------- |
| Purpose        | Decides what task should run             | Decides where task should run | Executes the task      |
| Responsibility | Monitors DAGs and creates task instances | Sends tasks to workers        | Runs the actual code   |
| Analogy        | Manager                                  | Dispatcher                    | Employee               |
| Example        | Task A is ready to run                   | Send Task A to Worker 1       | Run Task A Python code |

---

## 2. Variables vs XComs vs Params

| Feature | Variables                 | XComs                                      | Params                |
| ------- | ------------------------- | ------------------------------------------ | --------------------- |
| Purpose | Store global values       | Share data between tasks                   | Pass runtime inputs   |
| Scope   | Across all DAGs           | Within DAG run                             | DAG run               |
| Storage | Airflow Metadata DB       | Airflow Metadata DB                        | DAG configuration     |
| Example | `bucket_name=prod_bucket` | Task A sends `record_count=1000` to Task B | `run_date=2026-06-24` |

---

## 3. DAG vs Task vs Operator

| Feature  | DAG                   | Task               | Operator                |
| -------- | --------------------- | ------------------ | ----------------------- |
| Purpose  | Complete workflow     | Single work item   | Template to create task |
| Contains | Multiple tasks        | One operation      | Task logic              |
| Example  | Customer ETL Pipeline | Load Customer File | PythonOperator          |

---

## 4.  LocalExecutor vs CeleryExecutor vs KubernetesExecutor

| Feature     | LocalExecutor              | CeleryExecutor                                 | KubernetesExecutor                    |
| ----------- | -------------------------- | ---------------------------------------------- | ------------------------------------- |
| Execution   | Same machine               | Multiple workers                               | Separate pod per task                 |
| Scalability | Medium                     | High                                           | Very High                             |
| Best For    | Small projects             | Enterprise projects                            | Cloud-native projects                 |
| Example     | 10 tasks run on one server | Tasks distributed to Worker1, Worker2, Worker3 | Each task gets its own Kubernetes Pod |

---

## 5.  start_date vs execution_date vs Actual Run Time

| Feature    | start_date             | execution_date               | Actual Run Time                      |
| ---------- | ---------------------- | ---------------------------- | ------------------------------------ |
| Meaning    | When scheduling begins | Logical date being processed | Real execution time                  |
| Defined By | Developer              | Scheduler                    | System Clock                         |
| Example    | `2026-06-01`           | `2026-06-10` data processing | Task starts at `2026-06-11 00:05 AM` |

---

## 6.  schedule_interval vs @once vs None

| Feature    | schedule_interval | @once                         | None                    |
| ---------- | ----------------- | ----------------------------- | ----------------------- |
| Scheduling | Repeated schedule | Single run                    | No automatic schedule   |
| Trigger    | Automatic         | Automatic once                | Manual only             |
| Example    | `@daily`          | Run one time after deployment | User clicks Trigger DAG |

---

## 7.  Catchup vs Backfill vs Manual Trigger

| Feature      | Catchup                                         | Backfill                    | Manual Trigger          |
| ------------ | ----------------------------------------------- | --------------------------- | ----------------------- |
| Purpose      | Run missed schedules                            | Re-run historical data      | Run immediately         |
| Initiated By | Scheduler                                       | User                        | User                    |
| Example      | DAG paused for 5 days → runs all 5 missed dates | Re-run Jan 1 to Jan 10 data | Click "Trigger DAG" now |

---

## 8.  max_active_runs vs concurrency vs parallelism

| Feature  | max_active_runs                                | concurrency                                    | parallelism                                          |
| -------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------------- |
| Controls | Active DAG runs                                | Active tasks in one DAG                        | Active tasks in Airflow                              |
| Scope    | DAG level                                      | DAG level                                      | Airflow level                                        |
| Example  | `max_active_runs=2` → only 2 DAG runs together | `concurrency=5` → only 5 tasks of DAG together | `parallelism=50` → Airflow runs max 50 tasks overall |

---

## 9.  Retry vs Reschedule vs Restart

| Feature | Retry                           | Reschedule                                     | Restart                               |
| ------- | ------------------------------- | ---------------------------------------------- | ------------------------------------- |
| Purpose | Handle failures                 | Wait and check later                           | Run again                             |
| Trigger | Automatic                       | Automatic                                      | Manual                                |
| Example | Task fails → retry after 5 mins | File not available → check again after 10 mins | User clears failed task and reruns it |

---
# 10. Sensor Poke Mode vs Reschedule Mode

| Feature              | Poke Mode                                                | Reschedule Mode                                     |
| -------------------- | -------------------------------------------------------- | --------------------------------------------------- |
| Worker Usage         | Occupies worker continuously                             | Releases worker while waiting                       |
| Resource Consumption | High                                                     | Low                                                 |
| Best For             | Short waiting time                                       | Long waiting time                                   |
| Example              | Check every 30 sec for file arrival and keep worker busy | Check every 30 sec and free worker until next check |

---

# 11. PythonOperator vs BashOperator vs TaskFlow API

| Feature      | PythonOperator                      | BashOperator                   | TaskFlow API                       |
| ------------ | ----------------------------------- | ------------------------------ | ---------------------------------- |
| Executes     | Python function                     | Shell/Bash command             | Python function using decorators   |
| Coding Style | Traditional                         | Shell scripts                  | Modern Airflow style               |
| XCom Support | Manual                              | Limited                        | Automatic                          |
| Example      | Run Python data validation function | Execute `hdfs dfs -ls` command | `@task` function returning records |

---

# 12. BranchPythonOperator vs ShortCircuitOperator

| Feature          | BranchPythonOperator                         | ShortCircuitOperator                        |
| ---------------- | -------------------------------------------- | ------------------------------------------- |
| Purpose          | Choose one path among multiple branches      | Continue or stop workflow                   |
| Return Value     | Task ID(s)                                   | True/False                                  |
| Downstream Tasks | Selected branch runs                         | All downstream run or skip                  |
| Example          | If region=US → run US task, else run UK task | If file exists=True continue, else stop DAG |

---

# 13. Airflow Connections vs Variables vs Secrets Backend

| Feature  | Connections                 | Variables                  | Secrets Backend                       |
| -------- | --------------------------- | -------------------------- | ------------------------------------- |
| Purpose  | Store connection details    | Store configuration values | Store sensitive credentials securely  |
| Contains | Host, Username, Password    | Config values              | Passwords, API Keys, Tokens           |
| Security | Medium                      | Low                        | High                                  |
| Example  | BigQuery connection details | `project_id=prod`          | Secret stored in Vault/Secret Manager |

---

# 14. SLA vs Execution Timeout

| Feature | SLA                                        | Execution Timeout                   |
| ------- | ------------------------------------------ | ----------------------------------- |
| Purpose | Monitor delays                             | Stop long-running tasks             |
| Action  | Sends alert                                | Fails task                          |
| Impact  | Does not stop task                         | Terminates task                     |
| Example | Task should finish within 30 mins or alert | Kill task if running beyond 30 mins |

---

# 15. Task Timeout vs DAG Timeout

| Feature    | Task Timeout                    | DAG Timeout                           |
| ---------- | ------------------------------- | ------------------------------------- |
| Applies To | Single task                     | Entire DAG run                        |
| Scope      | Task level                      | Workflow level                        |
| Failure    | Task fails                      | DAG run fails                         |
| Example    | Task must finish within 10 mins | Entire DAG must finish within 2 hours |

---

# 16. TriggerDagRunOperator vs ExternalTaskSensor

| Feature    | TriggerDagRunOperator | ExternalTaskSensor                |
| ---------- | --------------------- | --------------------------------- |
| Purpose    | Start another DAG     | Wait for another DAG              |
| Action     | Active trigger        | Passive monitoring                |
| Dependency | Creates dependency    | Observes dependency               |
| Example    | DAG A triggers DAG B  | DAG A waits until DAG B completes |

---

# 17. TaskGroups vs SubDAGs

| Feature     | TaskGroups                   | SubDAGs                             |
| ----------- | ---------------------------- | ----------------------------------- |
| Purpose     | Visual grouping              | Separate DAG inside DAG             |
| Performance | Lightweight                  | Heavy                               |
| Recommended | Yes                          | No (Deprecated)                     |
| Example     | Group Extract tasks together | Create nested DAG for Extract phase |

---

# 18. Dynamic DAGs vs Dynamic Task Mapping

| Feature      | Dynamic DAGs                       | Dynamic Task Mapping                              |
| ------------ | ---------------------------------- | ------------------------------------------------- |
| Created When | DAG parse time                     | DAG run time                                      |
| Purpose      | Generate DAG structure dynamically | Generate tasks dynamically                        |
| Flexibility  | Lower                              | Higher                                            |
| Example      | Create 50 DAGs from config file    | Create tasks for 100 incoming files automatically |

---

# 19. Batch Processing in Airflow vs Streaming Processing in Dataflow

| Feature          | Airflow Batch Processing          | Dataflow Streaming Processing    |
| ---------------- | --------------------------------- | -------------------------------- |
| Data Type        | Historical data                   | Real-time data                   |
| Processing Style | Scheduled jobs                    | Continuous processing            |
| Latency          | Minutes/Hours                     | Seconds/Milliseconds             |
| Example          | Load daily sales file at midnight | Process Pub/Sub events instantly |

---

# 20. Apache Airflow vs Cloud Composer

| Feature        | Apache Airflow                   | Cloud Composer                             |
| -------------- | -------------------------------- | ------------------------------------------ |
| Type           | Open-source workflow tool        | Managed Airflow service on GCP             |
| Infrastructure | User manages                     | Google manages                             |
| Scaling        | Manual                           | Automatic                                  |
| Maintenance    | User responsibility              | Google responsibility                      |
| Example        | Install Airflow on VM/Kubernetes | Create Composer environment in GCP Console |

---

